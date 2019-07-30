# Source control Best Practices

**1. Commit Related Changes**

A commit should be a wrapper for related changes. For example, fixing two different bugs should produce two separate commits.

**2. Commit Often**

Committing often keeps your commits small and, again, helps you commit only related changes. Moreover, it allows you to share your code more frequently with others.

**3. Don’t Commit Half-Done Work**

**4. Test Before You Commit**

Resist the temptation to commit something that you “think” is completed. Test it thoroughly to make sure it really is completed and has no side effects \(as far as one can tell\).

**5. Write Good Commit Messages**

Begin your message with a short summary of your changes \(up to 50 characters as a guideline\). Separate it from the following body by including a blank line. The body of your message should provide detailed answers to the following questions: What was the motivation for the change? How does it differ from the previous implementation? Use the imperative, present tense \(„change“, not „changed“ or „changes“\) to be consistent with generated messages from commands like git merge.

**6. Use Branches**

Branches are the perfect tool to help you avoid mixing up different lines of development. You should use branches extensively in your development workflows: for new features, bug fixes, ideas…

**7. Agree on a Workflow**

Git lets you pick from a lot of different workflows: long-running branches, topic branches, merge or rebase, git-flow… However you choose to work, just make sure to agree on a common workflow that everyone follows.

