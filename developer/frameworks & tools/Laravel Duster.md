## \***\*Lint and Fix Your Laravel Code with Duster\*\***

Today Tighten **[announced the 1.0 release of Laravel-focused code linter and fixer Duster](https://tighten.com/insights/announcing-duster-a-laravel-code-linter-and-fixer/)**.

**[Duster](https://github.com/tighten/duster)** is a tool that brings together **[Laravel Pint](https://laravel.com/docs/pint)**, **[PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)**, **[PHP-CS-Fixer](https://github.com/PHP-CS-Fixer/PHP-CS-Fixer)**, and Tighten's Laravel-specific lints in **[Tlint](https://github.com/tighten/tlint)** to provide a powerful and comprehensive linting and fixing toolset for Laravel apps.

If you've read our articles about **[sharing PHPCS rules](https://laravel-news.com/sharing-phpcs-rules)** or **[sharing PHP-CS-Fixer rules](https://laravel-news.com/sharing-php-cs-fixer-rules-across-projects-and-teams)**, you're already familiar with the idea of publishing a set of your own rules for your projects. Duster takes Laravel's base opinions in Pint and then adds the power of additional linters and fixers through the other three tools it bundles. By default it sticks to **[Tighten's code style](https://github.com/tighten/duster/blob/main/style-guide.md)**, but it's also completely configurable to your preferences.

Let's take a look at how to install Duster, how to run it, how to integrate it into your automated workflows, and how to to configure it (if you want--you may be happy with its default rules!)

### Installing Duster

There are a few ways you can run Duster on your application, but the simplest way to start is to install it as a Composer dependency in your app.

```bash
composer require tightenco/duster --dev
```

You don't need to publish or configure anything; Duster comes with an opinionated set of styles out of the box, and if you like them, it's ready to go as soon it finishes installing.

### Running Duster

There are two main features Duster provides: "linting" and "fixing". Lints tell you when something in your code is out of sync with a rule; fixing fixes that code.

First, we can do the basics: Linting or fixing the entire codebase.

If we run **`lint`**, it'll give us a lint of the entire codebase, running all the linting tools:

```
./vendor/bin/duster lint
```

This will give us the output for each tool, and, like any linter, will return with a success or failure code that can be used in CI tools or other scripts.

We can also run **`fix`** to tell all the included tools to fix any issues they can in the entire codebase:

```
./vendor/bin/duster fix
```

### Only linting “dirty” files

When introducing a linter/fixer to an existing codebase, it can often seem overwhelming: there are so many little fixes you need to make you may be tempted to throw the entire thing away.

One way you can avoid running any fixes (or getting a ton of lint failures) for code that you're not working on at the moment is Duster's **`--dirty`** flag, which only runs the linters/fixers on files that have un-committed changes.

```
./vendor/bin/duster lint --dirty
./vendor/bin/duster fix --dirty
```

### Why fixing and linting?

There are two main reasons why Duster, and many tools like it, offer both linting and fixing. Why add linting when you can always just fix everything?

First, some teams may prefer a workflow where incorrect code is surfaced as a failing build (e.g. as a GitHub Action) instead of fixed.

And second, some lints can't be fixed automatically. A computer can tell if your code is broken but isn't smart enough to fix it for you.

## \***\*Integrating Duster Into Your CI\*\***

Like most code analysis tools, Duster's **`lint`** command returns a success or error code based on whether the lints succeeded. This means you can use **`./vendor/bin/duster lint`** in any CI pipeline to fail your builds if your lints aren't matched. You can also use **`./vendor/bin/duster fix`** as a part of a Husky hook or a CI hook to automatically format your code.

If you use GitHub Actions, Duster makes it easy to publish an action configuration that will either **`lint`** your code or **`fix`** it. Run **`./vendor/bin/duster github-actions`** and follow the prompts there to add the GitHub Action to your codebase.

## \***\*Configuring Duster (and its tools)\*\***

Like Pint, Duster embodies the opinions of its creators (Tighten) about how code should be styled. But Duster itself, and each of the tools it imports, can be configured to your liking.

### **duster.json**

Duster provides its own configuration file, **`duster.json`**. This file allows you to define files and folders to **`include`** or **`exclude`** from the Laravel-default files it targets by default. You can also use it to define additional scripts you'd like to run as a part of your **`duster`** flow.

For example, you can add **[PHPStan](https://phpstan.org/)** to your **`lint`** command with the following **`duster.json`**:

```
{
    "scripts": {
        "lint": {
            "phpstan": ["./vendor/bin/phpstan", "analyse"]
        }
    }
}

```

You can also define your own custom additions to the **`fix`** command.

### **Duster's dependencies**

You can configure each of Duster's dependencies with their native configuration files; you can learn more about how in the **[Customizing section of the Duster readme](https://github.com/tighten/duster#customizing)**.

- Pint: **`pint.json`**
- PHP_CodeSniffer: **`.phpcs.xml.dist`**
- PHP-CS-Fixer: **`.php-cs-fixer.dist.php`**
- Tlint: **`tlint.json`**
