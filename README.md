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


`git submodule add <URL> / <path>`


## Hazards

## Summary


