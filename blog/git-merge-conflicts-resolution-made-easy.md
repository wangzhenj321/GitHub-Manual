It’s the end of the day. You just finished some important work in your git feature branch. Your code is working beautifully. Unit tests are passing. Code reviewers approved. All is green. Time to merge!

> Automatic merge failed; fix conflicts and then commit the result.

At that moment, you feel a mix of despair, fear, and anger. Anger for that co-worker who dared to edit the same lines as you and merged their own feature branch five minutes earlier, leaving you the pleasure to handle the merge conflict. But it doesn’t have to be this way.

Let’s take a look at this merge conflict and see how it should be fixed:

```
<<<<<<< feature_branch

Alice asked her father if she could
borrow his motorbike. He said ok but told

=======

Alice asked her parents if she could
borrow their car. They said ok but told

>>>>>>> master

her she had to be back by 11pm.
```

Here we tried to merge “feature_branch” into “master”.

The part between `<<<<<<< feature_branch` and `=======` represents the state of the code in `feature_branch`. These two lines are conflicting with the lines between `=======` and `>>>>>>>` master that were changed in the master branch.

So did Alice ask her father for the motorbike? Or her parents for the car? Or maybe it was her father for the car? There is no way to know. All we can be sure of is that Alice must be back by 11pm.

There is no way to know because the context is missing. We know that the two conflicting lines were both modified in `master` and in `feature_branch`, but we don’t know how they were modified. All we can see is their current state in each branch.

This is where the git setting `merge.conflictStyle` can help. Let’s set it to “diff3”:

```
git config --global merge.conflictstyle diff3
```

Now let’s attempt the same merge again. This time, the conflict looks like this:

```
<<<<<<< feature_branch

Alice asked her father if she could
borrow his motorbike. He said ok but told

||||||| merged common ancestors

Alice asked her father if she could
borrow his car. He said ok but told

=======

Alice asked her parents if she could
borrow their car. They said ok but told

>>>>>>> master

her she had to be back by 11pm.
```

There is now a new section between `||||||| merged common ancestors` and `=======`. This section represents the state of the code in the nearest common ancestors.

If the git history looks like this:

The nearest common ancestor between `feature_branch` and `master` is commit “A”.

And now we know exactly what happened.

- Initially, at commit “A”: Alice was asking her father about the car.
- By comparing the `merged common ancestors` code with the `master` one, we can deduce that in `master` it was decided that Alice wouldn’t ask only her father, but her parents.
- By comparing the `merged common ancestors` code with the `feature_branch` one, we can deduce that in `feature_branch` the car was replaced by the motorbike.

As a result, we now know that the right way to resolve the conflict is to have Alice asking her parents about the motorbike.

And still be back by 11pm.

## References

1. [Git Merge conflicts resolution made easy](https://devblog.classy.org/git-merge-conflicts-resolution-made-easy-f44d9fbd7fec)
