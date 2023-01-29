# Welcome

This is a backend repository of the [wisniewski-mateusz.github.io/submodulesIES/](https://wisniewski-mateusz.github.io/submodulesIES/) site. It is a result of working on project about git submodules. It contains (at least should) all the necessary information about them.

# Submodules
## Introduction

Submodules, in short, is the concept which allows for reusing code over multiple projects. Such a concpet is used as a means to keep the working repository structured and maintained. It simply refers to a directory within the project which in fact is a different git repository. This wiki will shortly describe the setting for appropriate application, the fundamentals, the process of application and the hazards associated with such application. 

## Conditional setting

Before considering the application of such a concept as submodules, one ought to ask him/herself when it can be appropriate. Often, it is very dependent on the technology or framework which is used in the working repo. Namely, 

## Fundamentals

Before discussing the fundamentals of submodules the outsourced code from a different repo will be referred to as a module and the working repo in which such module is used will be considered the container repo. 

The concept of submodules is associated with the term nesting repos. In other words, there exists a module subject to the container repo for which the module in turn has its own repo. Nevertheless, in accordance with the concept of submodules, both the module repo and the container repo ought to act independently. Therefore, it follows that both have independent working with different logs. 

For further information, one ought to note that the submodule commit is stored through SHA1. Such storage method allows for the module to not automatically update. This might be considered inconveniant at first, but the opposite couldn't be more true as automatic updates of the module allow for serious complications in the implementation. 

## Application

First, a submodule needs to be added in *main* which is practically the container. Such submodule can be added through the following command:

`git submodule add <URL><path>`

Furthermore, one can observe that either a URL or path ought to be specified. The URL should be used in case the module repo is a remote repo. Moreover, the path should be specified in case the module repo is stored locally. When conducting such command, the `git status` command will indicate to a new *.gitmodules* file. In case of a locally specified path this illustrates the local config. This is helpful as the collaborators on the project can now use the mechanism of the *.gitmodules* file for which they can obtain the already defined submodules which they now can register in their own repositories. In practice, when working in the *main*, it is hard to keep track of the according logs of the submodule for which it is recommended to set up the following commnand:

`git config --global status.submoduleSummary true` 

It will allow us to observe the submodule status when conducting `git status` which was previously not possible. This makes it much easier for efficient and continuous utilization of submodules of the kind. Now, please note we have been working with 2 different repos but how exactly does the creation of a submodules represent in both the container repo and the submodule's repo? Well, the answer is simple, 


`git clone - recursive <URL> [<path>]`

## Hazards

## Summary
