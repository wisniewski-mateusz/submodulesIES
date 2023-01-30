---
layout: single
title: ""
permalink: /
toc: True
toc_label: "Table of contents"
toc_icon: "fas fa-list-ul"
toc_sticky: true
---

<span style="font-size:xx-large;">**How to work with submodules?**</span>

This site contains all the necessary information (available till 26th October) about Git submodules. It was based mostly on the [Git Pro - Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) section from `Git Pro` book. It is assumed that the reader knows basics of Git. If not, [here](https://martinhronec.github.io/JEM224/) is an introduction.

## 1. "Real-life" example

Before dealing with some definitions and other theoretical stuff, let's start with sketching an example of how someone can take advantage of git submodule(s). Assume that we are developing some websites and are in the backend team responsible for the website workflow and structure. The team doesn't want to be involved in anything connected with working on the content. Having a widely extended website, it would be a challenge to arrange the work of two groups, one mentioned and the second responsible for content creation. All those branches and subbranches to take care of. Why don't split this work into two repositories (site_repo, content_repo) and connect content_repo to the site_repo, arranging a fully functioning system? Site_repo would have one extra folder from which content would be taken, whereas content_repo wouldn't have anything additional. No one from this team would have the possibility of mistakenly changing something in some `.css` file and breaking half of the site functionality.

This kind of combined workflow has been added to this site. If you click on the `Entertainment` bar in the top right corner, you will see pages which haven't been created inside [this repository](https://github.com/wisniewski-mateusz/submodulesIES), but in [another](https://github.com/wisniewski-mateusz/submodulesIES_entertainment). However, it should be highlighted, that in this case, usage of the git submodule was a form over substance. Connecting these two repos and working on them simultaneously on one computer while choosing high-quality memes was annoying. Before starting to implement some new tool, one should always ask oneself if it is a good idea and then make another minimal mistake. [^1]

<p align="center">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/sad_meme.png" alt="alt_text" width="600"/>
</p>

The question is, how this kind of functionality can be created? Before answering it, let's catch up on some concepts.

## 2. Introduction

<p align="center">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/submodules_1.png" alt="alt_text" width="600"/>
</p>

Image taken from [this site](https://www.oreilly.com/library/view/version-control-with/9781449345037/ch17.html).

Submodule(s), in short, is the concept which allows for reusing code over multiple projects. Such a concept is used as a means to keep the working repository structured and maintained. It simply refers to a directory within the project, which is a different git repository. This wiki describes the setting for the appropriate application, the fundamentals, and the application. In the end, the table with listed commands is attached, and two exercises are formulated.

## 3. Conditional setting

Before considering the application of such a concept as submodule(s), one ought to ask him/herself when it can be appropriate. Often, it depends on the technology or framework used in the working repo. Namely, a lot of time, submodule(s) arises in the form of packages. If the project ought to use a decentralized source of code on which it can be dependent, then submodule(s) is an ideal method for efficient working. It would work as a supplementary package upon which it can be built in an efficient and organized manner.

## 4. Fundamentals

Before discussing the fundamentals of submodules, the outsourced code from a different repo will be referred to as a module, while the working repo in which such module is used will be considered the container repo.

The concept of submodules is associated with the nesting repos term. In other words, there exists a container repo that depends on some module which has its own repo. Nevertheless, in accordance with the concept of submodules, both the module repo and the container repo ought to act independently. Therefore, it follows that both have independent working with different logs.

For further information, one should note that the submodules' commit is stored through SHA1. Such a storage method doesn't allow for the module to update automatically. It might be considered inconvenient at first, but the opposite couldn't be more true as automatic updates might result in serious complications in the implementation.

<p align="center">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/submodules_2.png" alt="alt_text" width="600"/>
</p>

Image taken from [this site](https://www.oreilly.com/library/view/version-control-with/9781449345037/ch17.html).

## 5. Application

### 5.1. Adding a submodule

First, a submodule needs to be added in the *main* branch (or *master*, depending on when the repository has been created), which is practically the container. Such submodule can be added through the following command:

```
git submodule add <URL><path>
```

Furthermore, one can observe that either a URL or path ought to be specified. The URL should be used in case the module repo is a remote repo. Moreover, the path should be specified in case the module repo is stored locally. When conducting such a command, the `git status` command will point to a new *.gitmodules* file. In the case of a locally specified path, this illustrates the local config. It is helpful as the collaborators on the project can now use the mechanism of the *.gitmodules* file for which they can obtain the already defined submodule(s), which they can register in their repositories. In practice, when working in the *main*, it is hard to keep track of the according logs of the submodule for which it is recommended to set up the following command:

```
git config --global status.submoduleSummary true
```

It will allow us to observe the submodule status when conducting `git status`, which was previously impossible. It makes it much easier for efficient and continuous utilization of submodules of this kind. Please note we have been working with two different repos, but how exactly the creation of a submodule is represented in both the container repo and the submodule's repo? Well, the answer is simple, since the aim is to centralize the submodule(s) in the container repo, it is not stored spread over the working directory but rather in the *.git* directory. Furthermore, for the case of the submodule(s) repo, a reference is placed under the name of *gitdir*. Intuitively, by creating such branches, it is easier to find such logs of submodule(s) rather than having to look for them all over the working directory. It allows for working in a more structured and efficient manner. 

### 5.2. Cloning repos with active submodules

Having added a submodule in the repo, we now have to understand how one can reuse such a repo. Namely, when working as a team on a project, if a colleague attempts to clone the repository with the submodule through the `git clone` command, the submodule won't be present. Such submodule can be retrieved through the *.gitmodules*, which was mentioned before. Particularly such submodule can be retrieved through the following command:

```
git submodule init
```

This command allows the cloned repo to observe the submodule in question. However, it is not yet fetched, meaning the relevant commits are missing. To obtain such commits, one ought to manually retrieve them through:

```
git submodule update
```

Obviously, for practical purposes, one conducts the following command to obtain and update in one singular action:

```
git submodule update --init
```

Through such a command, we managed to manually obtain the submodule in the cloned repo as well as retrieve the relative contents. Please note that such a process is still inefficient, especially when working on bigger projects where multiple submodules might be needed. Therefore, we can optimize such processes by automatically updating and retrieving the submodules when cloning a repo through the *--recursive* option in the following command:

```
git clone - recursive <URL> [<path>]
```

However, note that when conducting such a command, the `git status` command will illustrate that the *HEAD* is detached.

### 5.3. Updating submodules in an active container

As we have now established how to add a submodule and clone the relative repo, important to understand is how to pull a repo with an active submodule. When using the usual `git pull` command, it, fortunately, fetches the submodules automatically as well as the other relative content. However, it does not automatically update the submodule. Namely, the remote repo of the submodule is updated locally, but the working repo did not update. Hence, we should update the submodule manually through the `git submodule update — init — recursive` (or the less optimal `git submodule update`) command. Unlike the case for cloning, there is no command automating the update of the submodule(s). However, there are some alternative methods, such as custom scripts, aliases and more, but this will not be discussed in this wiki.

Now we will discuss the case of updating the submodule in an active container. Imagine a scenario where two commits are made both in the container and the submodule repo. Following the commits, the pushes obviously have to be made too. At first, this conduct should lead to no errors on the surface. However, when checking the `git status`, a warning illustrates that the commit for the submodules got lost and is hence impossible to retrieve. Henceforth, it is crucial to also push the submodule in question as this was not conducted earlier and hence led to the error. For easier and more efficient use, the following CLI option aids in not forgetting about pushing the submodule too:

```
git config --global alias.spush 'push --recurse-submodules=on-demand'
```

### 5.4. Removing a submodule

In order to remove a submodule(s), there are two different approaches. One can either remove it temporarily or permanently. Removing a submodule temporarily is the easiest way, as it can be conducted by the following command:

```
git submodule deinit
```

Such a command causes the submodule to be locally ignored, which results in the submodule no longer being present in the `git status`. In addition, any *git submodules* command following the *git submodule deinit* command will ignore the temporarily removed submodule in question. Important to note is that the ignored submodule can still be referenced and retrieved in the *.gitmodules* file. The submodule can henceforth be instigated once again using the following command below.

```
git submodule update --init
```

In the case of permanently removing the submodule, it is slightly more complicated. In addition to removing the submodule from the working directory, we also have to remove it from the *.gitmodules* file. 

```
git rm <path-to-submodule>
```

The above command does exactly so. In fact, it removes the module entirely. 

## 6. Final remarks

In summary, this wiki illustrates a brief overview of the working of submodules. Firstly, a real-life working example of the usage of submodules was shown. Then, it was discussed for which setting a submodule might be useful, with the most common format in which it arises. Further, the fundamentals were briefly described on which the section of the application is based. Finally, cloning a repo with an active submodule, updating submodules in an active container, and removing submodules were discussed. Please refer to the following links for further information on the matter in question:

- [Mastering Git submodules](https://medium.com/@porteneuve/mastering-git-submodules-34c65e940407),
- [Working with git submodules](https://medium.com/fiverr-engineering/working-with-git-submodules-ec6210801e07),
- [Git book](https://git-scm.com/book/en/v2).

## 7. Useful commands

Here all the helpful commands described in this wiki are listed. Check the table below.




| Command                       | Purpose                                       |
|-------------------------------|-----------------------------------------------|
| `git submodule add <URL><path>` | Add the submodule to the container repository |
| `git submodule update`          | Update the submodule by the latest commits    |
| `git submodule init` | Initialize the submodule using the credits from the *.gitmodules* file |
| `git submodule update --init` | Combine commands submodule init and submodule update |
| `git clone - recursive <URL> [<path>]` | Clone the repository with all nested submodules |
| `git submodule deinit` | Remove the submodule temporarily |
| `git rm <path-to-submodule>` | Remove the submodule permanently |
| `git config --global status.submoduleSummary true` | Allow to observe the submodule status with `git status` |
| `git config --global alias.spush 'push --recurse-submodules=on-demand'` | Allow to push simultaneously commits from container repo and submodule |

## 8. Exercises

Here are a few exercises which can help you practice newly acquired skills. Good luck!

### 8.1. Ex. 1

Fork the repositories: [submodulesIES_submodule](https://github.com/wisniewski-mateusz/submodulesIES_submodule) and [submodulesIES_container](https://github.com/wisniewski-mateusz/submodulesIES_container). In the `submodulesIES_submodule` repository a python script with the definition of the function `is_it_prime` can be found. This function checks whether the given number is a prime number. Whereas the `submodulesIES_container` repository contains a python script which requires the definition of this function in order to work properly. Your task is to add `submodulesIES_submodule` as a submodule of `submodulesIES_container` and assure yourself that `main.py` from `submodulesIES_container` works as it should.

### 8.2. Ex. 2

You realized that function `is_it_prime` from the `submodulesIES_submodule` repository is not defined optimally. Why, while having a number $n$ and trying to check if it is a prime number, one would consider all the numbers $\\{2, ..., n-1\\}$ as potential factors instead of taking $\\{2, ..., \lfloor\sqrt{n}\rfloor\\}$? Considering an example of the huge prime number such as 7,263,497,693,459,281, this approach would be a significant optimization since $\lfloor\sqrt{n}\rfloor=85,226,156$, so we have got 7,263,497,608,233,125 fewer numbers to check. Your task is to update the `submodulesIES_submodule` repository by replacing the `is_it_prime` definition into:

```py
def is_it_prime(n: int) -> bool:
    for i in range(2, int(n ** .5)):
        if not n % i:
            return False
    return True
```

After that, you should pull those changes to the `submodulesIES_container` repository and assure yourself that everything works as it should.

### 8.3. Ex. 3

This time you realized that it was a form over substance to have those two repositories to obtain such functionality. Firstly, your task is to temporarily delete the submodule from `submodulesIES_container` and make `main.py` workable without it. After that, you should initialize the submodule back and delete it permanently. Of course, the `main.py` should still work as before.

---
---

[^1]: A small (minimal?) pun, since website is powered by [minimal mistakes](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/).