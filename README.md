<!--
#
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
-->

# Apache Attic Website

This is the source code for the website at [attic.apache.org](https://attic.apache.org)
which manages ASF projects which have retired.

This site uses [Jekyll](https://github.com/jekyll/jekyll), which is a static site generator.
See the [Jekyll Website](https://jekyllrb.com/) on how to install Jekyll and build this
site locally.

## TODO
This Poc is functional but there are a number of tasks remaining:
  - Create data files for all Attic projects (currently only 13 are done)
  - Convert XDOC home & process pages to markdown
  - Fix the Look & Feel
    - currently using the default Jekyll **Minima** theme
    - need to decide how the website should look and fix the page layout and how it looks
    - add standard "Apache" links
  - Decide whether the **flag** functionality should be included
  - decide what to do about **revived** projects. From what I can see only
    **XMLBeans** & **Ambari** have been revived. We don't include Ambari but we
    have a page for XMLBeans (I think we don't bother with them)


## Overview

The [Attic Website](https://attic.apache.org) is composed of the following:

  - Simple `markdown` pages such as the _home_ (`index.md`) and _Process_ (`process.md`) pages.
  - A `yaml` file for each project in the `_data/projects` directory which contains all the
    details about the project and its retirement
  - The _Process Tracking_ (`tracking.md`) page which generates a table showing the status of each
    project generated from the files in `_data/projects' directory.
  - (Jekyll Plugins)[https://jekyllrb.com/docs/plugins/] which generate pages and files for the
    retired projects from the files in `_data/projects' directory:
    - `_plugins/projects-plugin.rb` generates the (project pages)[https://attic.apache.org/projects/]
      from the project's `yaml` data file.
    - `_plugins/attic-banner-plugin.rb` generates a _flag_ file to indicate that the _Attic Banner_
      should be added to a project's website (based on the project's `yaml` data file).
    - `_plugins/cwiki-banner-plugin.rb` generates a _flag_ file to indicate that the _Attic Banner_
      should be added to the project's CWIKI spaces (based on the project's `yaml` data file).

## Project YAML Data File

The project YAML files contain the following information in order to generate the project pages:
  - **Retirement Date**
  - **JIRA ID** of the ticket used to track the project's move to the Attic
  - **Completion Date** of the project's move to the Attic
  - **Project Description**
  - **Source Code** repositories
  - **Mailing Lists**
  - **Issue Trackers**
  - **Wiki** spaces
  - **Download Details**
  - **Related Projects**

Creating/Updating a project's YAML file updates the project page, updates the Tracking page
and generates any required flags for the project's website and wiki.

```yaml
retirement_date:                 ### [REQUIRED] Date the project retired (yyyy-mm-dd)                             
attic_issue:                     ### [OPTIONAL] The JIRA-ID managing the projects retirement
attic_date:                      ### [OPTIONAL] Date the move to the Attic was completed (yyyy-mm-dd)
attic_banner:                    ### [OPTIONAL] Valid values: true/false
project_name:                    ### [OPTIONAL] defaults to the file name
project_domain:                  ### [OPTIONAL] defaults to the file name + ".apache.org"
project_description: >-
    [Put some text here]
additional_text: >-
    [Put some text here]
board_resolution:                ### [REQUIRED] Valid values: true/false
board_reports:                   ### [REQUIRED] Valid values: true/false
downloads:                       ### [REQUIRED] Valid values: true/false
archive_path:                    ### [OPTIONAL] Defaults to the file name
source_repositories:
    - type:                      ### [REQUIRED] Valid Values: Subversion, Git
      path:                      ### [OPTIONAL] Defaults to the file name
mailing_lists:
    - dev
    - commits
    - user
mailing_lists_prefix:            ### [OPTIONAL] Defaults to the file name
issue_tracker:
    type: JIRA                   ### [REQUIRED] Valid Values: JIRA
    keys:                        ### [OPTIONAL] Defaults to this file name
      -
      -
wiki:
    type: CWIKI                  ### [REQUIRED] Valid values: CWIKI
    keys:                        ### [OPTIONAL] Defaults to the file name
      -
      -
related_projects_text: >-
    [Put some text here]         ### [OPTIONAL]
related_projects:
    - name:                      ### [OPTIONAL]
      url:                       ### [OPTIONAL]
      description:           
```

Heres an example of a file for **Any23**:

```yaml
retirement_date: 2023-06-21
attic_issue: ATTIC-215
attic_date: 2023-10-01
attic_banner: true 
project_description: >-
    The mission of Apache Any23 (Anything to Triples) was the creation and
    maintenance of software related to automatic crawling, parsing, analyzing,
    producing, validating and converting RDF (Resource Description Framework) data.
board_resolution: true
board_reports: true
downloads: true
source_repositories:
    - type: Git
mailing_lists:
    - dev
    - commits
    - user
issue_tracker:
    type: JIRA
wiki:
    type: CWIKI

```
