# PHP Widgets

A comprehensive, object-oriented Bootstrap 5 component library for PHP. Build clean, maintainable HTML components with a fluent, chainable API.
---

## Table of Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Architecture Overview](#architecture-overview)
- [Components](#components)
  - [Button](#button)
  - [Alert](#alert)
  - [Card](#card)
  - [Badge](#badge)
  - [Breadcrumb](#breadcrumb)
  - [Form](#form)
  - [Input](#input)
  - [Select](#select)
  - [Textarea](#textarea)
  - [Modal](#modal)
  - [Nav](#nav)
  - [ProgressBar](#progressbar)
  - [ListGroup](#listgroup)
- [Layout System](#layout-system)
  - [Container](#container)
  - [Grid System](#grid-system)
  - [Layout Helpers](#layout-helpers)
- [ComponentsFactory](#componentsfactory)
- [Form Handling](#form-handling)
- [Helpers](#helpers)
  - [Attributes](#attributes)
  - [Classes](#classes)
- [Base Classes](#base-classes)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- **Full Bootstrap 5 Support** — All major components with complete styling options
- **Fluent API** — Chainable methods for elegant, readable code
- **Composable** — Nest components freely to build complex layouts
- **Responsive Grid** — Complete grid system with breakpoints, offsets, and ordering
- **Built-in Security** — HTML escaping, CSRF protection, and SQL injection detection
- **Form Validation** — Comprehensive form handler with validation rules
- **Factory Methods** — Quick component creation with shorthand helpers
- **Extensible** — Abstract base classes make adding new components easy
- **Zero Dependencies** — Pure PHP with no external runtime requirements

---

## Requirements

- PHP 8.0 or higher
- Bootstrap 5.x CSS and JavaScript (loaded in your HTML template)

---

## Installation

### Via Composer

```bash
composer require mlangeni/machinjiri-widgets
```

### Manual Installation

Clone or download the library and include the autoloader:

```php
require_once 'path/to/vendor/autoload.php';
```

### Bootstrap Assets

Include Bootstrap in your HTML template:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

---

## Quick Start

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Button;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Card;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Container;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Layout;

// Simple button
echo (new Button('Click Me'))->primary()->large()->render();

// Card with content
$card = (new Card())
    ->header('Featured')
    ->title('Welcome')
    ->text('This is a Bootstrap card built with PHP Widgets.')
    ->footer('Updated today');

echo $card->render();

// Full layout
$container = Layout::container();
$container->addContent($card->render());
echo $container->render();
```

---

## Architecture Overview

```
Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\
├── Base\
│   ├── ComponentBase.php       # Abstract base with attributes/classes/styles
│   └── ComponentTrait.php      # Shared rendering helpers
├── Components\                  # UI components
│   ├── Alert.php
│   ├── Badge.php
│   ├── Breadcrumb.php
│   ├── Button.php
│   ├── Card.php
│   ├── Form.php
│   ├── Input.php
│   ├── ListGroup.php
│   ├── Modal.php
│   ├── Nav.php
│   ├── ProgressBar.php
│   ├── Select.php
│   └── Textarea.php
├── Layout\
│   ├── Container.php
│   ├── Grid.php                 # Grid, Row, Column
│   └── Layout.php               # Layout facade/helpers
├── Helpers\
│   ├── Attributes.php
│   └── Classes.php
├── Forms\
│   └── FormHandler.php
└── ComponentsFactory.php
```

### Core Concepts

| Concept | Description |
|---------|-------------|
| **ComponentBase** | Abstract class providing attribute, class, and style management |
| **ComponentTrait** | Provides `renderElement()` for HTML output |
| **Fluent API** | Every setter returns `$this` for method chaining |
| **render()** | Every component exposes `render()` returning an HTML string |

---

## Components

### Button

Create styled buttons, including links and submit buttons.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Button;

// Basic button
$btn = (new Button('Submit'))->primary()->render();

// Variants
(new Button('Primary'))->primary();
(new Button('Secondary'))->secondary();
(new Button('Success'))->success();
(new Button('Danger'))->danger();
(new Button('Warning'))->warning();
(new Button('Info'))->info();
(new Button('Light'))->light();
(new Button('Dark'))->dark();
(new Button('Link'))->link();

// Outline style
(new Button('Outline'))->primary()->outline();

// Sizes
(new Button('Small'))->primary()->small();
(new Button('Large'))->primary()->large();

// Block-level
(new Button('Full Width'))->primary()->block();

// Disabled
(new Button('Disabled'))->primary()->disabled();

// As a link
(new Button('Go Home'))->primary()->asLink('/home');

// As a submit button
(new Button('Save'))->success()->asSubmit();

// As reset
(new Button('Reset'))->secondary()->asReset();

// With custom attributes
$btn = (new Button('Click'))
    ->primary()
    ->setAttribute('id', 'my-btn')
    ->setAttribute('data-action', 'save')
    ->render();
```

---

### Alert

Display contextual feedback messages.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Alert;

// Basic alert
$alert = (new Alert('Operation completed!'))->success()->render();

// Variants
(new Alert('Info'))->info();
(new Alert('Warning'))->warning();
(new Alert('Error'))->danger();

// Dismissible
$alert = (new Alert('This can be closed'))
    ->success()
    ->dismissible()
    ->render();

// With icon
$alert = (new Alert('Saved successfully'))
    ->success()
    ->withIcon('bi bi-check-circle')
    ->render();
```

---

### Card

Build flexible content containers.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Card;

$card = (new Card())
    ->header('Card Header')
    ->title('Card Title')
    ->subtitle('Supporting subtitle')
    ->text('Some quick example text to build on the card title.')
    ->footer('Footer content')
    ->render();

// With image
$card = (new Card())
    ->image('/images/photo.jpg', 'Photo', true) // true = top
    ->title('Image Card')
    ->text('Description text')
    ->render();

// Colored card
$card = (new Card())
    ->primary()
    ->title('Primary Card')
    ->text('Text')
    ->render();

// With body items (raw HTML)
$card = (new Card())
    ->title('Custom Body')
    ->addBodyItem('<a href="#" class="btn btn-primary">Action</a>')
    ->render();

// With list items
$card = (new Card())
    ->header('Tasks')
    ->addListItems(['Task 1', 'Task 2', 'Task 3'])
    ->render();
```

Available color variants: `primary()`, `secondary()`, `success()`, `danger()`, `warning()`, `info()`, `light()`, `dark()`.

---

### Badge

Small status indicators and labels.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Badge;

$badge = (new Badge('New'))->primary()->render();
$badge = (new Badge('Alert'))->danger()->pill()->render();
```

---

### Breadcrumb

Navigation breadcrumbs.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Breadcrumb;

$breadcrumb = (new Breadcrumb())
    ->addItem('Home', '/')
    ->addItem('Products', '/products')
    ->addItem('Details', '/products/123', true) // last = active
    ->render();
```

---

### Form

Wrapper for form fields.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Form;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Input;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Button;

$form = (new Form())
    ->method('post')
    ->action('/submit')
    ->needsValidation()
    ->addFields([
        (new Input('email'))->email()->label('Email')->required()->render(),
        (new Input('password'))->password()->label('Password')->required()->render(),
        (new Button('Login'))->primary()->asSubmit()->render(),
    ]);

echo $form->render();
```

---

### Input

Text inputs with labels, help text, and validation states.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Input;

// Text
$input = (new Input('username'))
    ->text()
    ->label('Username')
    ->placeholder('Enter your username')
    ->required()
    ->render();

// Email
$input = (new Input('email'))->email()->label('Email Address')->render();

// Password
$input = (new Input('password'))->password()->label('Password')->render();

// Number
$input = (new Input('age'))->number()->label('Age')->render();

// Date
$input = (new Input('birthday'))->date()->label('Birthday')->render();

// File
$input = (new Input('avatar'))->file()->label('Profile Picture')->render();

// Checkbox
$input = (new Input('terms'))->checkbox()->label('I agree')->render();

// With help text
$input = (new Input('phone'))
    ->text()
    ->label('Phone')
    ->helpText('Include country code.')
    ->render();

// Floating label
$input = (new Input('name'))
    ->text()
    ->label('Your Name')
    ->floatingLabel()
    ->render();

// Sizes
$input = (new Input('name'))->text()->size('sm')->render();  // Small
$input = (new Input('name'))->text()->size('lg')->render();  // Large

// Readonly
$input = (new Input('id'))->text()->value('123')->readonly()->render();
```

---

### Select

Dropdown selections.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Select;

$select = (new Select('country'))
    ->options([
        'us' => 'United States',
        'ca' => 'Canada',
        'uk' => 'United Kingdom',
    ])
    ->label('Country')
    ->render();
```

---

### Textarea

Multi-line text input.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Textarea;

$textarea = (new Textarea('message'))
    ->rows(5)
    ->label('Message')
    ->placeholder('Write your message...')
    ->render();
```

---

### Modal

Dialog overlays.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Modal;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Button;

$modal = (new Modal('deleteModal'))
    ->title('Confirm Delete')
    ->body('Are you sure you want to delete this item?')
    ->footer(
        (new Button('Cancel'))->secondary()->setData('bs-dismiss', 'modal')->render() .
        (new Button('Delete'))->danger()->render()
    )
    ->centered()
    ->render();

// Trigger
echo '<button type="button" class="btn btn-danger" data-bs-toggle="modal" data-bs-target="#deleteModal">Delete</button>';
echo $modal;
```

Methods:
- `title()`, `body()`, `footer()`
- `staticBackdrop()` — Prevent closing on backdrop click
- `centered()` — Vertically center the modal
- `scrollable()` — Enable scrolling for long content
- `size('sm'|'lg'|'xl')` — Modal size

---

### Nav

Navigation menus, tabs, and pills.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Nav;

$nav = (new Nav())
    ->addItem('Home', '/', true)  // active
    ->addItem('About', '/about')
    ->addItem('Contact', '/contact')
    ->render();

// Tabs
$tabs = (new Nav())
    ->tabs()
    ->addItem('Profile', '#profile', true)
    ->addItem('Settings', '#settings')
    ->render();

// Pills
$pills = (new Nav())
    ->pills()
    ->addItem('Tab 1', '#tab1', true)
    ->addItem('Tab 2', '#tab2')
    ->render();

// Vertical
$nav = (new Nav())->vertical()->addItem('Item', '#')->render();

// Justified (equal width)
$nav = (new Nav())->justified()->addItem('A', '#')->addItem('B', '#')->render();
```

---

### ProgressBar

Display progress indicators.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\ProgressBar;

// Basic
$bar = (new ProgressBar(75))->primary()->render();

// With label
$bar = (new ProgressBar(60))
    ->success()
    ->showLabel()
    ->render();

// Striped + animated
$bar = (new ProgressBar(40))
    ->info()
    ->striped()
    ->animated()
    ->showLabel()
    ->render();

// Custom text
$bar = (new ProgressBar(80))
    ->warning()
    ->text('80% complete')
    ->render();
```

---

### ListGroup

Flexible list containers.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\ListGroup;

$list = (new ListGroup())
    ->addItem('Item 1', true)      // active
    ->addItem('Item 2')
    ->addItem('Item 3', false, true) // disabled
    ->render();
```

---

## Layout System

### Container

Bootstrap containers for content wrapping.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Container;

// Fixed-width container
$container = new Container();
$container->addContent('<p>Hello</p>');

// Fluid (full-width)
$container = (new Container())->fluid();

// Responsive breakpoint container
$container = (new Container())->responsive('md');

// Multiple contents
$container = (new Container())
    ->addContents(['<p>First</p>', '<p>Second</p>'])
    ->render();
```

---

### Grid System

Full grid with rows, columns, breakpoints, offsets, and ordering.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Grid;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Column;

$grid = new Grid();
$grid->addRow([
    ['content' => 'Column 1', 'size' => 4],
    ['content' => 'Column 2', 'size' => 4],
    ['content' => 'Column 3', 'size' => 4],
]);

echo $grid->render();
```

#### Building Columns Directly

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Column;

$col = (new Column())
    ->size(6)
    ->addContent('<p>Content</p>');

// Responsive breakpoints
$col = (new Column())
    ->size(12)
    ->breakpoint('md', 6)
    ->breakpoint('lg', 4)
    ->addContent('Responsive content');

// Offset
$col = (new Column())->size(6)->offset(3)->addContent('Centered');

// Responsive offset
$col = (new Column())->size(6)->offsetBreakpoint('md', 2);

// Ordering
$col = (new Column())->size(6)->order('first');
$col = (new Column())->size(6)->orderBreakpoint('md', 'last');

// Auto-size
$col = (new Column())->auto();
```

#### Row Helpers

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Row;

$row = new Row();
$row->addColumn($column1);
$row->addColumn($column2);
$row->alignItems('center');       // Vertical align: start|center|end
$row->justifyContent('between');  // Horizontal: start|center|end|between|around
$row->noGutters();
$row->gutterSize('g-3');

echo $row->render();
```

#### Gutter Configuration

```php
$grid = (new Grid())
    ->noGutters()                    // Remove all gutters
    ->gutterSize('g-2')              // Set uniform gutters
    ->verticalGutterSize('gy-3')     // Vertical gutters
    ->horizontalGutterSize('gx-5');  // Horizontal gutters
```

---

### Layout Helpers

High-level static helpers from the `Layout` facade.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Layout;

// Container
$container = Layout::container();
$fluid = Layout::fluidContainer();
$responsive = Layout::responsiveContainer('lg');

// Grid
$grid = Layout::grid();
$row = Layout::row([
    ['content' => 'A', 'size' => 6],
    ['content' => 'B', 'size' => 6],
]);
$column = Layout::column([
    'content' => 'Hello',
    'size' => 12,
    'breakpoints' => ['md' => 6, 'lg' => 4],
    'offset' => 2,
    'order' => 1,
]);
```

#### Two-Column Layout

```php
$html = Layout::twoColumn([
    'sidebarSize' => 3,
    'contentSize' => 9,
    'sidebarContent' => '<nav>Sidebar</nav>',
    'content' => '<main>Main content</main>',
    'sidebarBreakpoints' => ['md' => 4],
    'contentBreakpoints' => ['md' => 8],
    'fluid' => false,
]);
```

#### Three-Column Layout

```php
$html = Layout::threeColumn([
    'leftSize' => 2,
    'middleSize' => 7,
    'rightSize' => 3,
    'leftContent' => '<aside>Left</aside>',
    'middleContent' => '<main>Content</main>',
    'rightContent' => '<aside>Right</aside>',
]);
```

#### Hero Section

```php
$html = Layout::hero([
    'title' => 'Welcome to Our App',
    'subtitle' => 'Build amazing things fast',
    'content' => '<p>Get started today.</p>',
    'ctaButton' => '<a href="/signup" class="btn btn-light btn-lg">Sign Up</a>',
    'background' => 'bg-primary',
    'textColor' => 'text-white',
]);
```

#### Card Grid

```php
$html = Layout::cardGrid([
    'cards' => [
        $card1->render(),
        $card2->render(),
        $card3->render(),
    ],
    'breakpointColumns' => [
        'sm' => 1,
        'md' => 2,
        'lg' => 3,
        'xl' => 4,
    ],
]);
```

#### Form Layout

```php
$html = Layout::formLayout([
    'sidebar' => '<h3>Help</h3><p>Fill out the form.</p>',
    'form' => $form->render(),
    'sidebarSize' => 4,
    'formSize' => 8,
]);
```

---

## ComponentsFactory

A convenience factory class providing both constructor-style creation and shortcut helpers.

### Standard Factories

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\ComponentsFactory as UI;

UI::button('Click Me');
UI::alert('Message');
UI::card();
UI::form();
UI::input('email');
UI::progressBar(50);
UI::badge('New');
UI::modal('myModal');
UI::nav();
UI::select('country');
UI::textarea('notes');
UI::breadcrumb();
UI::listGroup();
```

### Quick Helpers

```php
// Primary button in one call
echo UI::primaryButton('Submit')->render();

// Dismissible success alert
echo UI::successAlert('Saved!')->render();

// Typed inputs with labels
echo UI::textInput('name', 'Full Name')->render();
echo UI::emailInput('email', 'Email Address')->render();
echo UI::passwordInput('password', 'Password')->render();
```

### Combining with Fluent API

```php
echo UI::button('Delete')
    ->danger()
    ->outline()
    ->setData('confirm', 'true')
    ->render();
```

---

## Form Handling

The `FormHandler` class processes incoming HTTP requests, validates input, and handles CSRF and SQL injection protection.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Forms\FormHandler;

$handler = new FormHandler();

// Define validation rules
$handler->setRules([
    'name' => 'required|min:3|max:100',
    'email' => 'required|email',
    'password' => 'required|min:8',
    'age' => 'required|numeric|min:18',
]);

// Custom messages
$handler->setMessages([
    'email' => [
        'required' => 'Email is required.',
        'email' => 'Please enter a valid email address.',
    ],
]);

// Field labels for friendlier error messages
$handler->setFieldLabels([
    'name' => 'Full Name',
    'email' => 'Email Address',
]);

// Validate
if (!$handler->validate()) {
    // Handle errors
    $errors = $handler->getErrors();
    $handler->redirectBack();
}

// Access validated data
$validated = $handler->getValidatedData();
$name = $handler->getValidatedData('name');

// Raw data access
$all = $handler->getData();
$email = $handler->getData('email', 'default@example.com');
```

### Configuration Methods

| Method | Description |
|--------|-------------|
| `setRules(array)` | Define validation rules per field |
| `setMessages(array)` | Custom validation error messages |
| `setFieldLabels(array)` | Friendly field labels |
| `enableCsrf(bool)` | Enable/disable CSRF verification |
| `sanitizeInput(bool)` | Enable/disable input sanitization (default: on) |
| `autoValidate(bool)` | Automatically validate on `handle()` |
| `storeOldInput(bool)` | Persist old input in session |

### Input Access Helpers

```php
$handler->getData();              // All input
$handler->getData('email');       // Single field
$handler->getValidatedData();     // Only validated fields
$handler->getErrors();            // All errors
$handler->getErrors('email');     // Errors for a field
$handler->hasErrors();            // Boolean
$handler->has('email');           // Field exists and not empty
$handler->filled('email');        // Field has a value (incl. '0')
$handler->only(['name', 'email']); // Whitelist fields
$handler->except(['password']);   // Blacklist fields
```

### HTTP Method Detection

```php
$handler->isPost();
$handler->isGet();
$handler->isPut();
$handler->isPatch();
$handler->isDelete();
$handler->getMethod();
```

### File Uploads

```php
$file = $handler->getFile('avatar');
$files = $handler->getFiles();
```

### Flash & Old Input

```php
// Flash a message
$handler->flash('success', 'Saved successfully!');

// Retrieve old input after redirect
$oldEmail = $handler->old('email', '');

// Explicitly persist input
$handler->withInput();

// Attach validation errors to session
$handler->withErrors(['email' => ['Invalid email']]);
```

### Responses

```php
// Redirect with flash data and old input
$handler->redirect('/dashboard');
$handler->redirectBack();

// JSON response with status/errors/data
$handler->jsonResponse(['id' => 42]);

// Pre-built responses
$handler->successResponse('Created!', $data);
$handler->errorResponse('Something went wrong', 422, $errors);
```

### CSRF Helper Fields

```php
// Hidden input for forms
echo $handler->csrfField();

// Meta tag for AJAX
echo $handler->csrfMeta();

// Method spoofing (PUT/PATCH/DELETE)
echo $handler->methodField('PUT');
```

### Typical Usage Pattern

```php
$handler = (new FormHandler())
    ->setRules([
        'email' => 'required|email',
        'password' => 'required|min:8',
    ])
    ->enableCsrf(true);

if ($handler->isPost()) {
    if ($handler->validate()) {
        // Process $handler->getValidatedData()
        $handler->redirect('/dashboard');
    }
    $handler->redirectBack();
}

// GET: render form
$form = (new Form())
    ->method('post')
    ->addFields([
        $handler->csrfField(),
        (new Input('email'))->email()->label('Email')->render(),
        (new Input('password'))->password()->label('Password')->render(),
        (new Button('Login'))->primary()->asSubmit()->render(),
    ]);

echo $form->render();
```

---

## Helpers

### Attributes

Merge and stringify HTML attributes.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Helpers\Attributes;

$attrs = Attributes::merge(
    ['class' => 'btn', 'type' => 'button'],
    ['id' => 'submit', 'disabled' => null] // null/empty values removed
);
// ['class' => 'btn', 'type' => 'button', 'id' => 'submit']

echo Attributes::toString($attrs);
// class="btn" type="button" id="submit"
```

### Classes

Merge class lists with deduplication.

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Helpers\Classes;

$classes = Classes::merge(
    ['btn', 'btn-primary'],
    ['btn-lg', 'btn-primary']  // duplicate removed
);
// ['btn', 'btn-primary', 'btn-lg']

echo Classes::toString($classes);
// btn btn-primary btn-lg
```

---

## Base Classes

### ComponentBase

Abstract foundation for all components. Provides:

| Method | Description |
|--------|-------------|
| `setId(string)` | Set the `id` attribute |
| `addClass(string)` | Append a CSS class |
| `addClasses(array)` | Append multiple CSS classes |
| `setAttribute(string, string)` | Set an HTML attribute |
| `setAttributes(array)` | Merge in multiple attributes |
| `setData(string, string)` | Set a `data-*` attribute |
| `setStyle(string, string)` | Set an inline style property |
| `render()` *(abstract)* | Return the component HTML |

Property access: `$this->attributes`, `$this->classes`, `$this->styles`, `$this->dataAttributes`.

### ComponentTrait

Provides `renderElement(string $tag, string $content = '', array $attributes = [])` for simple HTML tag generation with self-closing support for void elements (`input`, `img`, `br`, `hr`, `meta`, `link`).

### Extending

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Base\ComponentBase;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Base\ComponentTrait;

class Badge extends ComponentBase
{
    use ComponentTrait;

    private string $text = '';

    public function __construct(string $text = '', array $attributes = [])
    {
        parent::__construct($attributes);
        $this->text = $text;
        $this->addClass('badge');
    }

    public function primary(): self
    {
        $this->addClass('bg-primary');
        return $this;
    }

    public function pill(): self
    {
        $this->addClass('rounded-pill');
        return $this;
    }

    public function render(): string
    {
        return $this->renderElement('span', $this->text);
    }
}
```

---

## Examples

### Complete Login Page

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\{Form, Input, Button, Alert, Card};
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\{Layout, Column, Row};
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Forms\FormHandler;

$handler = (new FormHandler())
    ->setRules([
        'email' => 'required|email',
        'password' => 'required|min:8',
    ]);

$errorAlert = '';
if ($handler->isPost() && !$handler->validate()) {
    $errorAlert = (new Alert('Invalid credentials. Please check your input.'))
        ->danger()
        ->dismissible()
        ->render();
}

$loginCard = (new Card())
    ->header('Sign In')
    ->addBodyItem($errorAlert)
    ->addBodyItem(
        (new Form())
            ->method('post')
            ->action('/login')
            ->addFields([
                $handler->csrfField(),
                (new Input('email'))
                    ->email()
                    ->label('Email Address')
                    ->value($handler->old('email'))
                    ->required()
                    ->render(),
                (new Input('password'))
                    ->password()
                    ->label('Password')
                    ->required()
                    ->render(),
                '<div class="mt-3">' .
                    (new Button('Sign In'))->primary()->block()->asSubmit()->render() .
                '</div>',
            ])
            ->render()
    );

$column = (new Column())
    ->size(12)
    ->breakpoint('md', 6)
    ->offsetBreakpoint('md', 3)
    ->addContent($loginCard->render());

$row = (new Row())->addColumn($column);

$container = (new \Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Container())
    ->addClass('mt-5')
    ->addContent($row->render());

echo $container->render();
```

### Dashboard Layout

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Layout;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\{Card, ProgressBar, Badge};

$sidebar = '<h5>Navigation</h5><ul class="nav flex-column">'
    . '<li class="nav-item"><a class="nav-link active" href="#">Dashboard</a></li>'
    . '<li class="nav-item"><a class="nav-link" href="#">Users</a></li>'
    . '<li class="nav-item"><a class="nav-link" href="#">Settings</a></li>'
    . '</ul>';

$stats = (new Card())
    ->header('Server Load')
    ->addBodyItem((new ProgressBar(72))->success()->showLabel()->render())
    ->addBodyItem('<p class="mt-3">Status: ' . (new Badge('Healthy'))->success()->render() . '</p>')
    ->render();

echo Layout::twoColumn([
    'sidebarSize' => 3,
    'contentSize' => 9,
    'sidebarContent' => $sidebar,
    'content' => $stats,
    'sidebarBreakpoints' => ['md' => 3],
    'contentBreakpoints' => ['md' => 9],
    'fluid' => true,
]);
```

### Product Grid

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\Card;
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Layout;

$products = [
    ['name' => 'Widget Pro', 'price' => '$29.99'],
    ['name' => 'Widget Lite', 'price' => '$9.99'],
    ['name' => 'Widget Ultra', 'price' => '$59.99'],
    ['name' => 'Widget Mini', 'price' => '$4.99'],
];

$cards = array_map(function ($product) {
    return (new Card())
        ->image('/images/placeholder.jpg', $product['name'])
        ->title($product['name'])
        ->text($product['price'])
        ->addBodyItem('<a href="#" class="btn btn-primary btn-sm">Add to Cart</a>')
        ->render();
}, $products);

echo Layout::cardGrid([
    'cards' => $cards,
    'breakpointColumns' => ['sm' => 1, 'md' => 2, 'lg' => 4],
]);
```

### User Profile

```php
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Components\{Card, Badge, Button};
use Mlangeni\Machinjiri\Widgets\Modules\Bootstrap\Layout\Layout;

$profile = (new Card())
    ->header('User Profile')
    ->title('Jane Doe')
    ->subtitle('Senior Developer')
    ->text('Passionate about clean code and open-source software.')
    ->addBodyItem(
        (new Badge('Admin'))->primary()->render() . ' ' .
        (new Badge('Verified'))->success()->render() . ' ' .
        (new Badge('New'))->info()->render()
    )
    ->addBodyItem(
        '<div class="mt-3">' .
        (new Button('Edit Profile'))->primary()->render() . ' ' .
        (new Button('Sign Out'))->secondary()->outline()->render() .
        '</div>'
    )
    ->render();

echo Layout::responsiveContainer('md')
    ->addContent('<div class="mb-4">' . $profile . '</div>')
    ->render();
```

---

## Security Notes

- **Output escaping**: `renderElement()` uses `htmlspecialchars()` on attributes automatically. Text content passed to `Card::title()`, `Alert`, `Input::label()`, and similar setters is escaped via `htmlspecialchars()`.
- **Raw content**: Methods named `addBodyItem()`, `addContent()`, `addContents()`, and `body()` accept raw HTML strings by design. **Only pass trusted content.**
- **CSRF**: Use `FormHandler` with `enableCsrf(true)` and inject `csrfField()` into forms.
- **SQL injection**: `FormHandler` includes a heuristic `SQLInjectionChecker`. Always use parameterized queries — this is defense in depth, not a substitute.
- **Input sanitization**: `FormHandler::sanitizeInput(true)` is enabled by default and HTML-escapes all scalar input. Disable only if you handle escaping yourself.

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit changes: `git commit -am 'Add new component'`
4. Push: `git push origin feature/my-feature`
5. Open a Pull Request

Please follow PSR-12 coding standards and add tests for new components.

---

## License

MIT License. See [LICENSE](LICENSE) for details.

Copyright (c) Mlangeni Machinjiri

---

## Support

- **Issues**: [GitHub Issues](https://github.com/mlangeni-group/php-widgets/issues)
- **Documentation**: This README
- **Discussions**: [GitHub Discussions](https://github.com/mlangeni-group/php-widgets/discussions)

---