---
title: Manage a workspace with git
description: Learn how to connect a workspace to a git repo and branch, commit changes and sync.
author: mberdugo
ms.author: monaberdugo
ms.reviewer: NimrodShalit
ms.topic: how-to
ms.date: 05/30/2023
ms.custom: build-2023
---

# Manage a workspace with git

This article walks you through the following basic tasks in Microsoft Fabric’s git integration tool:

- [Connect to a git repo](#connect-a-workspace-to-an-azure-repo)
- [Commit changes](#commit-changes-to-git)
- [Update from git](#update-workspace-from-git)
- [Disconnect from git](#disconnect-a-workspace-from-git)

It’s recommended to read the [overview of git integration](./intro-to-git-integration.md) before you begin.

[!INCLUDE [preview-note](../../includes/preview-note.md)]

## Prerequisites

To integrate git with your Microsoft Fabric workspace, you need to set up the following prerequisites in both Azure DevOps and Fabric.

### Azure DevOps prerequisites

- An active Azure account registered to the same user that is using the Fabric workspace. [Create a free account](https://azure.microsoft.com/products/devops/).
- Access to an existing repository

### Fabric prerequisites

To access the git integration feature, you need one of the following licenses:

- [Power BI Premium license](/power-bi/enterprise/service-premium-what-is). Your Power BI premium license will continue to work for all Power BI features.
- [Fabric license](../../enterprise/licenses.md#capacity-and-skus). A Fabric license is necessary to use all supported Fabric items.

In addition, your organization’s administrator has to [enable the Fabric switch](../../admin/fabric-switch.md). If this switch is disabled, contact your administrator.

## Connect a workspace to an Azure repo

Only a workspace admin can connect a workspace to an [Azure Repo](/azure/devops/repos/get-started), but once connected, anyone with [permission](#permissions) can work in the workspace. If you're not an admin, ask your admin for help with connecting. To connect a workspace to an Azure Repo, follow these steps:

1. Sign into Power BI and navigate to the workspace you want to connect with.

1. Go to **Workspace settings**

    :::image type="content" source="./media/git-get-started/workspace-settings-new.png" alt-text="Screenshot of workspace with workspace settings icon displayed on top.":::

    > [!NOTE]
    > If you don't see the Workspace settings icon, select the ellipsis (three dots) the then workspace settings.
    > :::image type="content" source="./media/git-get-started/workspace-settings-link.png" alt-text="Screenshot of workspace with workspace settings link displayed from ellipsis.":::

1. Select **Git integration**. You’re automatically signed into the Azure Repos account registered to the Azure AD user signed into the workspace.

    :::image type="content" source="./media/git-get-started/workspace-settings.png" alt-text="Screenshot of workspace settings window with git integration selected.":::

1. From the dropdown menu, specify the following details about the branch you want to connect to:

    > [!NOTE]
    > You can only connect a workspace to one branch and folder at a time.

    - [Organization](/azure/devops/user-guide/plan-your-azure-devops-org-structure)
    - [Project](/azure/devops/user-guide/plan-your-azure-devops-org-structure#how-many-projects-do-you-need)
    - [Git repository](/azure/devops/user-guide/plan-your-azure-devops-org-structure#structure-repos-and-version-control-within-a-project)
    - Branch (Select an existing branch using the drop-down menu, or select **+ New Branch** to create a new branch. You can only be connected to one branch at a time.)
    - Folder (Select an existing folder in the branch or enter a name to create a new folder. If you don’t select a folder, content will be created in the root folder. You can only connect to one folder at a time.)

1. Select **Connect and sync**.

During the initial sync, if either the workspace or git branch is empty, content is copied from the nonempty location to the empty one. If both the workspace and git branch have content, you’re asked which direction the sync should go. For more information on this initial sync, see [Connect and sync](git-integration-process.md#connect-and-sync).

After you connect, the Workspace displays information about source control that allows the user to view the connected branch, the status of each item in the branch and the time of the last sync.

:::image type="content" source="./media/git-get-started/git-sync-information.png" alt-text="Screenshot of source control icon and other git information.":::

To keep your workspace synced with the git branch, [commit any changes](#commit-changes-to-git) you make in the workspace to the git branch, and [update your workspace](#update-workspace-from-git) whenever anyone creates new commits to the git branch.

## Commit changes to git

Once you successfully connect to a git folder, edit your workspace as usual. Any changes you save are saved in the workspace only. When you’re ready, you can commit your changes to the git branch, or you can undo the changes and revert to the previous status. Read more about [commits](git-integration-process.md#commit).

### [Commit to git](#tab/commit-to-git)

To commit your changes to the git branch, follow these steps:

1. Go to the workspace.
1. Select the **Source control** icon. This icon shows the number of uncommitted changes.
    :::image type="content" source="./media/git-get-started/source-control-number.png" alt-text="Screenshot of source control icon with the number 2 indicating that there are two changes to commit.":::
1. Select the **Changes** tab of the **Source control** pane.
   A list appears with all the items you changed, and an icon indicating if the item is *new* :::image type="icon" source="./media/git-get-started/new-commit-icon.png":::, *modified* :::image type="icon" source="./media/git-get-started/modified-commit-icon.png":::, *conflict* :::image type="icon" source="./media/git-get-started/conflict-icon.png":::, or *deleted* :::image type="icon" source="./media/git-get-started/deleted-commit-icon.png":::.
1. Select the items you want to commit. To select all items, check the top box.
1. Add a comment in the box. If you don't add a comment, a default message is added automatically.
1. Select **Commit**.

   :::image type="content" source="./media/git-get-started/commit-changes.png" alt-text="Screenshot of source control window with two changes selected to commit.":::

After the changes are committed, the items that were committed are removed from the list, and the workspace will point to the new commit that it's synced to.

:::image type="content" source="./media/git-get-started/no-changes.png" alt-text="Screenshot of source control window stating that there are no changes to commit.":::

After the commit is completed successfully, the status of the selected items changes from **Uncommitted** to **Synced**. 

### [Undo saved change](#tab/undo-save)

After saving changes to the workspace, if you decide that you don’t want to commit those changes to git, you can undo the changes and revert those items to the previous (unsaved) status. To undo your changes, follow these steps:

1. Go to the workspace.
1. Select the **Source control** button. This button also shows the number of uncommitted changes.
    :::image type="content" source="./media/git-get-started/source-control-number.png" alt-text="Screenshot of source control icon with the number 2 indicating that there are two changes to commit.":::
1. Select the **Changes** tab of the **Source control** pane.
   A list appears with all the items you changed, and an icon indicating if the changed item is *new* :::image type="icon" source="./media/git-get-started/new-commit-icon.png":::, *modified* :::image type="icon" source="./media/git-get-started/modified-commit-icon.png":::, *conflict* :::image type="icon" source="./media/git-get-started/conflict-icon.png":::, or *deleted* :::image type="icon" source="./media/git-get-started/deleted-commit-icon.png":::.
1. Select the changes you want to undo.
1. Select **Undo**.

   :::image type="content" source="./media/git-get-started/undo-changes.png" alt-text="Screenshot of source control window with two changes selected to undo.":::
1. Select **Undo** again to confirm.

   :::image type="content" source="./media/git-get-started/undo-confirm.png" alt-text="Screenshot of source control window asking if you're sure you want to undo changes.":::

The selected items in your workspace revert to how they were when the workspace was last synced.

> [!IMPORTANT]
> If you delete an item and then undo the changes, the item is created anew and some of the metadata might be lost. For example, the sensitivity labels aren’t kept and should be reset, and the owner of the item is set to the current user.

---

## Update workspace from git

Whenever anyone commits a new change to the connected git branch, a notification appears in the relevant workspace. Use the **Source control** pane to pull the latest changes, merges, or reverts into the workspace and update live items. Read more about [updating](git-integration-process.md#update).

To update a workspace, follow these steps:

1. Go to the workspace.
1. Select the **Source control** icon.
1. Select the **Updates** tab of the **Source control** pane. A list appears with all the items that were changed in the branch since the last update.
1. Select **Update all**.

:::image type="content" source="./media/git-get-started/source-control-update.png" alt-text="Screenshot of source control pane with the update tab open and the updating all button selected.":::

After it updates successfully, the list of items is removed, and the workspace will point to the new commit that it's synced to.

:::image type="content" source="./media/git-get-started/no-updates.png" alt-text="Screenshot of source control window stating that you successfully updated the workspace.":::

After the update is completed successfully, the status of the items changes to **Synced**.

## Disconnect a workspace from git

Only a workspace admin can disconnect a workspace from an Azure Repo. If you’re not an admin, ask your admin for help with disconnecting. If you’re an admin and want to disconnect your repo, follow these steps:

1. Go to Workspace settings
1. Select Git integration
1. Select **Disconnect workspace**

    :::image type="content" source="media/git-get-started/disconnect-workspace.png" alt-text="Screenshot of workspace settings screen with disconnect workspace option.":::

## Permissions

The actions you can take on a workspace depend on the permissions you have in both the workspace and Azure DevOps. For a more detailed discussion of permissions, see [Permissions](./git-integration-process.md#permissions).

## Considerations and limitations

If you're having trouble with these actions, make sure you understand the [limitations](./git-integration-process.md#considerations-and-limitations) of the git integration feature.

## Next steps

- [Understand the git integration process](./git-integration-process.md)
- [Manage git branches](./manage-branches.md)
- [Git integration best practices](../best-practices-cicd.md)
