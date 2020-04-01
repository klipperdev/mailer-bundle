Use the localizable Twig Doctrine loader
========================================

## Save localized templates

To use the localizable Twig Doctrine loader, you simply have to use the `@doctrine_template_message`
namespace to the name of the Template Message. Given that the translation is managed by the
Doctrine Extensions Translatable, each localized template message can be saved with the
workflow of this extension.

## Select a localized template

If the locale is not defined before the template name, the default locale is used:

```php
use Symfony\Bridge\Twig\Mime\TemplatedEmail;

$email = (new TemplatedEmail())
    // email config
    ->htmlTemplate('@user_templates/welcome')
;
```

To select manually the locale, you must add the valid locale in the path
(example `@user_templates/<LOCALE>/<TEMPLATE_NAME>`) like:

```php
use Symfony\Bridge\Twig\Mime\TemplatedEmail;

$email = (new TemplatedEmail())
    // email config
    ->htmlTemplate('@user_templates/fr_FR/welcome')
    // or
    ->htmlTemplate('@user_templates/fr/welcome')
;
```

Given that the translations is managed by Doctrine Extensions Translatable, the template
message repository of Klipper Mailer use the Query Hint with fallback to retrieved the localized template.

## Limit the template message by types

With the Doctrine entity of template message, you can defined the `type` (like email, sms, etc...),
and the Twig Loader can use this value in the criteria. The type can be added before or after the
locale, and like the locale, the type selector is optional, like:

```php
use Symfony\Bridge\Twig\Mime\TemplatedEmail;

$email = (new TemplatedEmail())
    // email config
    ->htmlTemplate('@user_templates/email/fr_FR/welcome')
    // or
    ->htmlTemplate('@user_templates/fr/email/welcome')
    // or
    ->htmlTemplate('@user_templates/email/welcome')
;
```

## Select a localized template with slash in template name

If you allow the slash in the template name, you must define the type in the path, even if the
type is empty, like:

```php
use Symfony\Bridge\Twig\Mime\TemplatedEmail;

$email = (new TemplatedEmail())
    // email config
    ->htmlTemplate('@user_templates/email/fr_FR/path/in/template/name')
    // or
    ->htmlTemplate('@user_templates/fr/email/path/in/template/name')
    // or
    ->htmlTemplate('@user_templates/email/path/in/template/name')
    // or without type filter
    ->htmlTemplate('@user_templates//path/in/template/name')
;
```
