# Github Projects

## Install

1. Copy this into your `{DRUPAL PATH}/sites/all/modules/githubprojects` directory. 
2. Open your modules tab and enable `Github Projects`. 
3. Click configure and paste a Github access token (from https://github.com/settings/applications).
4. Your nodes should now be populated.

## Uninstall

Delete the content type `githubproject`.

## Usage

Every hour the plugin will import all your github projects as nodes. This allows you to list and link to their pages locally.

## Extending 

To extend the type of content that is collected by the module: 

### 1. Add a field for the content to be stored

In `githubprojects.install` add another if statement of the form:

    if (!field_info_field('<MACHINE READBALE NAME>')) {

        $field = array(
            'field_name' => '<MACHINE READBALE NAME>',
            'type' => '<CONTENT TYPE>',
        );
        field_create_field($field);

        $instance = array(
            'field_name' => '<MACHINE READBALE NAME>',
            'entity_type' => 'node',
            'label' => '<LABEL>',
            'bundle' => 'githubproject'
        );
        field_create_instance($instance);

    }

 * `<MACHINE READABLE NAME>`: the machine readable name for the field, it must contain only letters and underscores; usually takes the form `githubprojects_<what is being stored>`
 * `<TYPE>`: The content type of what needs to be stored (i.e. text)
 * `<LABEL>`: The human readable label for the field

### 2. Actually store the content

In `githubprojects.module` in the `githubprojects_update_projects` function, add another line like:

    $node-><MACHINE READABLE NAME>['und'][0]['value'] = <VALUE>

 * `<MACHINE READABLE NAME>`: the machine readable name for the field, same as above
 * `<VALUE>`: The value to store, usually gotten from the github api (see the surrounding lines)

## Copyright

Copyright (c) 2013 The President and Fellows of Harvard College

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
