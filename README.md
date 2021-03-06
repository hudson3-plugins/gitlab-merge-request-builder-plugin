# Gitlab Merge Request Builder Plugin

A plugin that allows Hudson to build merge requests.

This plugin fetches the source and target branches of a Gitlab merge request and makes them available
to your build via build parameters. Once the build completes, Hudson will leave a comment on the merge
request indicating whether the merge request was successful.

## Prerequisites

* Whilst there is no explict dependency on the [Git plugin](http://wiki.hudson-ci.org/display/HUDSON/Git+Plugin),
  it's strongly recommended that you install it since Hudson will be unable to fetch the source code for your project.

## Installation

* Ensure that a Hudson user exists within Gitlab and has access to the repository. Ensure that the user
  has **Developer** level access to the project.
* Install the plugin in Hudson.
    * The plugin is hosted on the [Hudson Plugin repository](http://wiki.hudson-ci.org/display/HUDSON/Gitlab+Merge+Request+Builder+Plugin)
    * Go to ``Hudson`` -> ``Manage Hudson`` -> ``Manage Plugins`` -> ``Available``
    * Search for ``Gitlab Merge Request Builder``
    * And install it
    * Ensure you restart Hudson
* Go to ``Manage Hudson`` -> ``Configure System`` -> ``Gitlab Merge Requests Builder``
* Set the ``Gitlab Host URL`` to the base URL of your Gitlab server
* Set your ``Hudson Username`` for the Hudson user (defaults to jenkins)
* Set your ``Hudson API Token`` for the Hudson user. This can be found by logging into Gitlab as Hudson User
  and going to the user profile section
* Set/change any of the other available parameters as necessary. If you host Gitlab over an SSL connection
  you may want to enable ignoring certificate errors.
* ``Save`` to preserve your changes.

## Creating a Job

* Create a new job by going to ``New Job``
* Set the ``Project Name``
* Feel free to specify the ``GitHub Project`` url as the url for the Gitlab project (if you have the GitHub plugin installed)
* In the ``SCM`` section:
    * Click ``Git`` and enter your Repositroy URL and in Advanced set its Name to ``origin``
    * For merge requests from forked repositories add another repository with Repository URL ``${gitlabSourceRepository}`` and in Advanced set Name to ``${gitlabSourceName}``
    * In ``Branch Specifier`` enter ``origin/${gitlabSourceBranch}`` or for merge requests from forked repositories enter ``${gitlabSourceName}/${gitlabSourceBranch}``
    * Open the Advanced options
    * Tick the ``Merge before build`` option and specify the name of the repository as ``origin`` (if origin corresponds to Gitlab)
      and enter the ``Branch to merge to`` as ``${gitlabTargetBranch}``
    * **Ensure ``Prune remote branches before build`` is left unticked**
* In the ``Build Triggers`` section:
    * Check the ``Gitlab Merge Requests Builder``
    * Enter the ``Gitlab Project Path``, this might be something like ``gitlabhq/gitlabhq``
* Configure any other pre build, build or post build actions as necessary
* ``Save`` to preserve your changes

You can trigger a job a manually by clicking ``This build is parameterized`` and adding the relevant build parameters. These include:
* gitlabSourceBranch
* gitlabTargetBranch
* gitlabMergeRequestId

## Contributing

* Check out the latest master to make sure the feature hasn't been implemented or the bug hasn't been fixed yet
* Check out the issue tracker to make sure someone already hasn't requested it and/or contributed it
* Fork the project
* Start a feature/bugfix branch
* Commit and push until you are happy with your contribution
* Make sure to add tests for it. This is important so I don't break it in a future version unintentionally.
* Please try not to mess with the version, or history. If you want to have your own version, or is otherwise necessary, that is fine,
  but please isolate to its own commit so I can cherry-pick around it.

## Copyright

Copyright (c) 2013 Tim Olshansky. See LICENSE for further details.
