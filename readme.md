<p align="center">
<img width="200" src="https://raw.githubusercontent.com/JWardee/wp-mail-catcher/master/icon.svg?sanitize=true">
</p>

<h1 align="center">
WP Mail Catcher
</h1>

<p align="center">
Backup and save your contact form emails (including Contact Form 7) to your database with this fast, lightweight plugin (under 140kb in size!)
</p>

<p align="center">
<img src="https://github.com/JWardee/wp-mail-catcher/actions/workflows/main.yml/badge.svg">
</p>

## Features
* Zero setup required - just install and away you go
* Minimalistic - no overbloated features you never use weighing your site down - under 140kb in size!
* Bulk export emails to CSV for easy inclusion into Excel or any other program
* Compose new emails with the WordPress controls you're already familiar with
* Resend your emails in bulk
* Debugging - see exactly which file and code line was responsible for sending the email, along with any errors encountered
* Manage what user permissions can see the logs
* Routinely have your logs cleared out at a specified time - or keep them forever
* Need to be notified when there's a problem sending your mail? We've got hooks that allow you to do just that
* Completely free

![alt text](https://raw.githubusercontent.com/JWardee/wp-mail-catcher/master/build/images/wp-mail-catcher-screenshot-1.png)


![alt text](https://raw.githubusercontent.com/JWardee/wp-mail-catcher/master/build/images/wp-mail-catcher-screenshot-3.png)


![alt text](https://raw.githubusercontent.com/JWardee/wp-mail-catcher/master/build/images/wp-mail-catcher-screenshot-2.png)


![alt text](https://raw.githubusercontent.com/JWardee/wp-mail-catcher/master/build/images/wp-mail-catcher-screenshot-4.png)

## Confirmed support
* [wp_mail](https://developer.wordpress.org/reference/functions/wp_mail/)
* [WooCommerce](https://wordpress.org/plugins/woocommerce/)
* [Contact Form 7](https://wordpress.org/plugins/contact-form-7/)
* [MailGun](https://wordpress.org/plugins/mailgun/)
* [SparkPost](https://wordpress.org/plugins/sparkpost/)
* [Easy WP SMTP](https://wordpress.org/plugins/easy-wp-smtp/) (excluding their test email function)
* [SendGrid](https://en-gb.wordpress.org/plugins/sendgrid-email-delivery-simplified)
* [BuddyPress](https://en-gb.wordpress.org/plugins/buddypress/)
* Anything that uses wp_mail!

## Not currently supported
* [WP Mail Bank](https://wordpress.org/plugins/wp-mail-bank/) (unhooks wp_mail filters)
* [Post SMTP](https://wordpress.org/plugins/post-smtp/) (overrides wp_mail function and doesn't implement the same actions/filters)

## Hooks and actions
* `wp_mail_catcher_mail_success` is triggered when a message is sent and logged successfully. It has a single argument that is an array containing the log
  * `id` related to the id in the `mail_catcher_logs` MySQL table
  * `time` relative, readable time to when the log was saved
  * `email_to` the email address(es) that the message was sent to
  * `subject` the subject line of the message
  * `message` the contents of the message
  * `status` an integer depicting if the message was sent successfully or not (1 = sent successfully. 0 = sending failed)
  * `error` the error that occurred - if any
  * `backtrace_segment` a json_encoded object that shows which file and line the mail was initially triggered from
  * `attachments` a list of any attachments that were sent along with the email
  * `additional_headers` a list of any headers that were sent
  * `attachment_file_paths` a list of the location of any attachments that were sent
  * `timestamp` a unix timestamp of when the email was sent
  * `is_html` a boolean, that will be true if the message is a html email and false if not
  * `email_from` the from value of the email
* `wp_mail_catcher_mail_failed` is triggered when a message failed to send and logged successfully. It has a single argument that is an array containing the log (same as the arguments for `wp_mail_catcher_mail_success`)
* `wp_mail_catcher_deletion_intervals` is a filter that should return an array where each key is an amount of time in seconds, and the value is the label. Used to determine when a message has expired and should be deleted

## Developing locally
1. Download the repo
2. Install [Docker](https://www.docker.com/) and [Docker compose](https://docs.docker.com/compose/)
3. Allow entrypoint script to be executable `chmod +x ./entrypoint.sh`
4. Run `./entrypoint.sh up`
5. Go to `http://localhost:8080` and configure WordPress
6. Login to the admin panel and activate the plugin

## Extra commands
1. Run `./entrypoint.sh grunt compile` to compile assets
2. Run `./entrypoint.sh phpunit` to run unit tests
3. Run `./entrypoint.sh phpstan` to run static analysis
4. Run `./entrypoint.sh phpcs` to check linting
5. Run `./entrypoint.sh composer XYZ` to run composer (replace `XYZ` with your composer command)

## Changing PHP versions
1. Update the WordPress/PHP versions in the `entrypoint.sh` file. Ensure the [corresponding Docker image exists](https://hub.docker.com/_/wordpress/tags)
2. Destroy existing containers and their volumes
3. Run `./entrypoint.sh up`

## Found an issue, or have an idea on how we can improve?
Let us know in our [GitHub tracker!](https://github.com/JWardee/wp-mail-catcher/issues)

## Contributing
Contributions are always welcome, to get started do the following:
1. Complete "Developing locally steps", make any changes you need
2. Ensure unit tests pass (`./entrypoint.sh phpunit`)
3. Ensure static analysis pass (`./entrypoint.sh phpstan`)
4. Ensure code conforms to PSR-12 standard (`./entrypoint.sh phpcs`)
5. Submit your pull request!

## Additional resources
* [WordPress repository](https://wordpress.org/plugins/wp-mail-catcher/)
* [PSR-12 coding standards](http://www.php-fig.org/psr/psr-12/)
* [Installing composer](https://getcomposer.org/download/)
* [Installing grunt](https://gruntjs.com/getting-started/)

## Changelog
See the differences between versions [here](https://github.com/JWardee/wp-mail-catcher/releases)
