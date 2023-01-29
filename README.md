# Welcome

This is a backend repository of the [wisniewski-mateusz.github.io/submodulesIES/](https://wisniewski-mateusz.github.io/submodulesIES/) site. It is a result of working on project about git submodules. It contains (at least should) all the necessary information about them.

# Submodules
## Introduction

Submodules, in short, is the concept which allows for reusing code over multiple projects. Such a concpet is used as a means to keep the working repository structured and maintained. It simply refers to a directory within the project which in fact is a different git repository. This wiki will shortly describe the setting for appropriate application, the fundamentals, the process of application and the hazards associated with such application. 

## Conditional setting

Before considering the application of such a concept as submodules, one ought to ask him/herself when it can be appropriate. Often, it is very dependent on the technology or framework which is used in the working repo. Namely, often submodules arise in the from of packages. If the project ought to use a decentralized source of code which it can be dependent on, than submodules is an ideal method for efficient working. It would work as a supplementary packages for which it can be built upon in an efficient and organized manner.

## Fundamentals

Before discussing the fundamentals of submodules the outsourced code from a different repo will be referred to as a module and the working repo in which such module is used will be considered the container repo. 

The concept of submodules is associated with the term nesting repos. In other words, there exists a module subject to the container repo for which the module in turn has its own repo. Nevertheless, in accordance with the concept of submodules, both the module repo and the container repo ought to act independently. Therefore, it follows that both have independent working with different logs. 

For further information, one ought to note that the submodule commit is stored through SHA1. Such storage method allows for the module to not automatically update. This might be considered inconveniant at first, but the opposite couldn't be more true as automatic updates of the module allow for serious complications in the implementation. 

## Application

### Adding a submodule

First, a submodule needs to be added in *main* which is practically the container. Such submodule can be added through the following command:

`git submodule add <URL><path>`

Furthermore, one can observe that either a URL or path ought to be specified. The URL should be used in case the module repo is a remote repo. Moreover, the path should be specified in case the module repo is stored locally. When conducting such command, the `git status` command will indicate to a new *.gitmodules* file. In case of a locally specified path this illustrates the local config. This is helpful as the collaborators on the project can now use the mechanism of the *.gitmodules* file for which they can obtain the already defined submodules which they now can register in their own repositories. In practice, when working in the *main*, it is hard to keep track of the according logs of the submodule for which it is recommended to set up the following commnand:

`git config --global status.submoduleSummary true` 

It will allow us to observe the submodule status when conducting `git status` which was previously not possible. This makes it much easier for efficient and continuous utilization of submodules of the kind. Now, please note we have been working with 2 different repos but how exactly does the creation of a submodules represent in both the container repo and the submodule's repo? Well, the answer is simple, since the aim is to centralize the submodule(s) in the container repo, it is not stored spread over the working diretory but rather in the *.git* directory. Furthermore, for the case of the submodule repo, a reference is placed under the name of *gitdir*. Intuitively, by creating such branches it is just easier to find such logs of submodules rather than having to look for them all over the working directory. It allows for working in a more structured and efficient manner. 

### Cloning repos with active submodules

Having added a submodule in the repo, we now have to understand how one can reuse such a repo. Namely, when working as a team on a project, if a colleague attempts to clone the repository with the submodule, through the `git clone` command, the submodule will not be present. Such submodule can be retrieved through the *.gitmodules* which was talked about before. Particularly such submodule can be retrieved through the fllowing command:

`git submodule init`

This command allows the cloned repo to now be able to observe the submodule(s) in question, however, it is not yet fetched meaning that the relevant commits are missing. To obtain such commits one ought to manually retrieve them through:

`git submodule update`

Obviously, for practical purposes one normally just conducts the following command to obtain and update in one singular action:

`git submodule update --init`

Through such a command we managed to manually obtain the submodules in the cloned repo as well as retreive the relative contents. However, please note that such process is still inefficient aspecially when working on bigger projects where multiple submodules might be needed. Therefore, we can optimalize such processes through automatically updating and retrieving the submodule when cloning a repo through the *--recursive* option in the following command:

`git clone - recursive <URL> [<path>]`

However, please note that when conducting such a command the `git status` command will illustrate that the *HEAD* is detached.

### Updating submodules in an active container

As we have now established on how to add a submodule and clone the relative repo, important to understand is on how to pull a repo with an active submodule. When using the usual `git pull` command, it fortunately fetches the submodules automatically as well as the other relative content. However, it does not automatically update the submodule. Namely, the remote repo of the submodule is updated locally but the working repo did not update. Hence, we ought to update the submodule manually through the `git submodule update — init — recursive` (or the less optimal `git submodule update`) command. Unlike in the case for cloning, there is no command automating the update of the submodules in the case of cloning. However, there are some alternative methods such as custom script, aliases and more but this will not be discussed in this wiki. 

Now we will discuss the case of updating the submodule in an active container. Imagine a scenario where 2 commits are made both in the container and in the submodule repo. Following the commits, the pushes obviously have to be made too. At first this conduct should lead to no errors on the surface. However, when checking the `git status`, a warning illustrates that the commit for the submodules got lost and is hence not possible to retrieve. Henceforth, it is crucial to also push the submodule in question as this was not conducted earlier and hence led to the error in question. For easier and more efficient use, the following CLI option aids to not forget about pushing the submodule too:

`git config --global alias.spush 'push --recurse-submodules=on-demand'`

### Removing a submodule

In order to remove a submodule there are 2 different approaches. One can either remove it temporarilty or permanently. Removing a submodule temporarily is the easiest one as it can be conducted by the following simple command:

`git submodule deinit` 

Such command causes the submodule to be ignored locally and thus it would not be present in the `git status` no longer. In addition, any *git submodules* command following the *git submodule deinit* command will ignore the temporarily removed submodule in question. Important to note is that the ignored submodule can still be referenced and retrieved in the *.gitmodules* file. The submodule can henceforth be instigated once again using the following command:

`git submodule update --init`

In the case of temporarily removing the submodule it is slightly more complicated as in addition to removing the submodule from the working directory we also ought to remove it from the *.gitmodules* file. 

`git rm <path-to-submodule>`

The above command does exactly so. In fact it removes the module entirely. 


## Final remarks

In summary this wiki illustrates a brief overview of the working of submodules. First, it was discussed for which setting a submodule might be useful and the most common format in which it arises. Further, the fundamentals were briefly discussed for which the section of application is based upon. In the section of application adding submodules, cloning a repo with an active submodule, updating submodules in an active container and removing submodules were all discussed. Please refer to the following links for further information on the matter in question:

- [Mastering Git submodules](https://medium.com/@porteneuve/mastering-git-submodules-34c65e940407)
- [Working with git submodules](https://medium.com/fiverr-engineering/working-with-git-submodules-ec6210801e07)
- [Git book](https://git-scm.com/book/en/v2)

