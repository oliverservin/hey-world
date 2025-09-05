Now that Picstome offers handles for public profiles for photographers, the next best use case for this handle is to show bio links so that photographers can showcase their social profiles in one single place, just like an alternative to linktr.ee.

Customers should be able to create bio links, and we would show them in their Picstome public profile. It seems like a simple feature, but the implementation had a few challenges.

The first thing was to create a new Bio Link model with its corresponding migrations. I basically only needed two fields, a title and a URL, but I also needed a column to store the team ID to make the relationship with the customer's personal team and an order column for sorting links.

```php
// database/migrations/2025_09_04_002242_create_bio_links_table.php

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('bio_links', function (Blueprint $table) {
            $table->id();
            $table->foreignId('team_id')->constrained()->onDelete('cascade');
            $table->string('title');
            $table->string('url');
            $table->integer('order')->default(0);
            $table->timestamps();
        });
    }
};
```

The next step was to create a Laravel folio page so customers can manage their bio links, create, update, and delete them.

To add a new link, I used an add link action to simply store the add form and then reset the form fields. It uses a Livewire Form so that I can reuse this form logic for when editing bio links.

```php
// resources/views/pages/bio-links.blade.php

new class extends Component
{
    public BioLinkForm $addForm;

    public function addLink()
    {
        $this->addForm->store();
        $this->addForm->resetForm();
    }
}
```

The Form BioLinkForm doesn't exist yet, so I created it and added the title and URL field properties, the validation rules for the fields, the store method that validates the data, and lastly creates the bio link for the current user's team. Also, a helper to reset the form properties.

```php
class BioLinkForm extends Form
{
    public ?string $title = null;

    public ?string $url = null;

    protected function rules()
    {
        return [
            'title' => ['required', 'string', 'max:255'],
            'url' => ['required', 'url'],
        ];
    }

    public function store()
    {
        $this->validate();

        return Auth::user()->currentTeam->bioLinks()->create([
            'title' => $this->title,
            'url' => $this->url,
        ]);
    }

    public function resetForm()
    {
        $this->reset(['title', 'url']);
    }
}
```

For editing links, I'm thinking of using an inline edit, so that when the user clicks the edit link button, it shows the edit link fields inline instead of opening a new page. To support this, I need an edit link action in the Livewire component to first verify the user can edit the selected link with a bio link policy, assign the editing link that the user is actually editing, and populate the edit form with the selected link.

```php
// resources/views/pages/bio-links.blade.php

class BioLinkForm extends Form
{
    // ...

    public BioLinkForm $editForm;

    public ?BioLink $editingLink = null;

    public function editLink(BioLink $link)
    {
        $this->authorize('view', $link);

        $this->editingLink = $link;
        $this->editForm->setBioLink($link);
    }
}
```

```php
// app/Livewire/Forms/BioLinkForm.php

class BioLinkForm extends Form
{
    // ...

    public ?BioLink $bioLink = null;

    public function setBioLink(BioLink $bioLink)
    {
        $this->bioLink = $bioLink;

        $this->title = $bioLink->title;
        $this->url = $bioLink->url;
    }
}
```

Now I needed another action to actually save the new link data. First, use a policy to authorize the action, and use the bio link form to update the data, reset the form, and reset the currently editing link property.

```php
// resources/views/pages/bio-links.blade.php

new class extends Component
{
    // ...

    public function updateLink(BioLink $link)
    {
        $this->authorize('update', $link);
        $this->editForm->update();
        $this->editForm->resetForm();
        $this->editingLink = null;
    }
}
```

```php
// app/Livewire/Forms/BioLinkForm.php

class BioLinkForm extends Form
{
    // ...

    public ?BioLink $bioLink = null;

    public function update()
    {
        $this->validate();

        return $this->bioLink->update([
            'title' => $this->title,
            'url' => $this->url,
        ]);
    }
}
```

I also needed an action so the user can cancel the link edit if they prefer.

```php
// resources/views/pages/bio-links.blade.php

new class extends Component
{
    // ...

    public function cancelEdit(BioLink $link)
    {
        $this->editForm->resetForm();
        $this->editingLink = null;
    }
}
```

And lastly, be able to delete links.

```php
// resources/views/pages/bio-links.blade.php

new class extends Component
{
    // ...

    public function deleteLink(BioLink $link)
    {
        $this->authorize('delete', $link);
        $link->delete();
    }
}
```

Another thing I wanted to implement is letting the users reorder the links. After a bit of research, I came across an Alpine Sort plugin that would let users reorder the links, and to make it work, I need another Livewire action to change the link order by receiving the link and the new order from the Sort plugin.

```php
// resources/views/pages/bio-links.blade.php

new class extends Component
{
    // ...

    public function reorderLink(BioLink $link, int $newOrder)
    {
        $this->authorize('update', $link);
        $link->reorder($newOrder);
    }
}
```

I encapsulated the link reordering logic in a method in the Bio Link model. I'm pretty proud of this refactor, actually.

```php
// app/Models/BioLink.php
class BioLink extends Model
{
    // ...

    public function reorder(int $newOrder): void
    {
        $currentOrder = $this->order;

        if ($newOrder > $currentOrder) {
            $this->team->bioLinks()
                ->where('order', '>', $currentOrder)
                ->where('order', '<=', $newOrder)
                ->decrement('order');
        } elseif ($newOrder < $currentOrder) {
            $this->team->bioLinks()
                ->where('order', '>=', $newOrder)
                ->where('order', '<', $currentOrder)
                ->increment('order');
        }

        $this->update(['order' => $newOrder]);
    }
}
```

It took me some iterations to finally get to this point, but it was really worth it. The backend implementation looks clear and easy to maintain. Feel free to fully check out the pull request.

Next steps are to improve the UX of link management on mobile devices, since it uses tables that imply horizontal scrolling. Also, add more functionality to the public profile by adding, in addition to the bio link, social links and a bio description.
