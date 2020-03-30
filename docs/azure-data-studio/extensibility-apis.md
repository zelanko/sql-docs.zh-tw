---
title: 擴充性 API
titleSuffix: Azure Data Studio
description: 了解適用於 Azure Data Studio 的擴充性 API
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 8a4ebe26cbbf768222c7b97b95fa7df238faded3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75001893"
---
# <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 擴充性 API

[!INCLUDE[name-sos](../includes/name-sos.md)] 提供 API，供延伸模組用來與 Azure Data Studio 的其他部分 (例如物件總管) 互動。 這些 API 可從 [`src/sql/azdata.d.ts`](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/azdata.d.ts) 檔案取得，如下所述。

## <a name="connection-management"></a>連線管理
`azdata.connection`

### <a name="top-level-functions"></a>最上層函數

- `getCurrentConnection(): Thenable<azdata.connection.Connection>`：根據使用中的編輯器或物件總管選取項目，取得目前的連線。

- `getActiveConnections(): Thenable<azdata.connection.Connection[]>`：取得使用者的所有使用中連線清單。 如果沒有這類連線，會傳回空白清單。

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>`：取得字典，其中包含與連線相關聯的認證。 這些會當做 `azdata.connection.Connection` 物件下的選項字典一部分傳回，但會從該物件中移除。 

### `Connection`
- `options: { [name: string]: string }`：連線選項的字典
- `providerName: string`：連線提供者的名稱 (例如"MSSQL")
- `connectionId: string`：連線的唯一識別碼

### <a name="example-code"></a>範例程式碼
```
> let connection = azdata.connection.getCurrentConnection();
connection: {
    providerName: 'MSSQL',
    connectionId: 'd97bb63a-466e-4ef0-ab6f-00cd44721dcc',
    options: {
        server: 'mairvine-sql-server',
        user: 'sa',
        authenticationType: 'sqlLogin',
        ...
    },
    ...
}
> let credentials = azdata.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>物件總管

`azdata.objectexplorer`


### <a name="top-level-functions"></a>最上層函數
- `getNode(connectionId: string, nodePath?: string): Thenable<azdata.objectexplorer.ObjectExplorerNode>`：取得對應至指定連線和路徑的物件總管節點。 如果沒有指定路徑，會傳回指定連線的最上層節點。 如果指定的路徑中沒有節點，會傳回 `undefined`。 注意:物件的 `nodePath` 是由 SQL 工具服務後端所產生，很難以手動方式建構。 未來的 API 改進將可讓您根據所提供的節點相關中繼資料 (例如名稱、類型和結構描述) 來取得節點。

- `getActiveConnectionNodes(): Thenable<azdata.objectexplorer.ObjectExplorerNode>`：取得所有使用中的物件總管連線節點。

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<azdata.objectexplorer.ObjectExplorerNode[]>`：尋找符合指定中繼資料的所有物件總管節點。 當 `schema`、`database` 和 `parentObjectNames` 引數不適用時，應該是 `undefined`。 `parentObjectNames` 是從物件總管最頂層到最底層的非資料庫父物件清單，所需物件會位於下方。 例如，搜尋屬於資料表 "schema1.table1" 和資料庫 "database1" 且具有連線識別碼 `connectionId` 的資料行 "column1" 時，請呼叫 `findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`。 另請參閱此 API 呼叫的[預設 Azure Data Studio 支援類型清單](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API)。

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string`：節點所在的連線識別碼

- `nodePath: string`：節點的路徑，用於呼叫 `getNode` 函數。

- `nodeType: string`：表示節點類型的字串

- `nodeSubType: string`：表示節點子類型的字串

- `nodeStatus: string`：表示節點狀態的字串

- `label: string`：顯示在物件總管中的節點標籤

- `isLeaf: boolean`：節點是否為分葉節點，因此沒有子系

- `metadata: azdata.ObjectMetadata`：描述此節點所表示物件的中繼資料

- `errorMessage: string`：節點處於錯誤狀態時顯示的訊息

- `isExpanded(): Thenable<boolean>`：節點目前是否在物件總管中已展開

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>`：設定要展開或摺疊節點。 如果狀態設定為 [無]，則不會變更節點。

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>`：設定是否選取節點。 如果 `clearOtherSelections` 為 true，會在進行新的選取時清除其他選取項目。 如果為 false，則會保留所有現有的選取項目。 當 `selected` 為 true 時，`clearOtherSelections` 預設為 true；當 `selected` 為 false 時，預設為 false。

- `getChildren(): Thenable<azdata.objectexplorer.ObjectExplorerNode[]>`：取得此節點的所有子節點。 如果沒有子系，會傳回空白清單。

- `getParent(): Thenable<azdata.objectexplorer.ObjectExplorerNode>`：取得此節點的父節點。 如果沒有父系，會傳回 undefined。

### <a name="example-code"></a>範例程式碼

```cs
private async interactWithOENode(selectedNode: azdata.objectexplorer.ObjectExplorerNode): Promise<void> {
    let choices = ['Expand', 'Collapse', 'Select', 'Select (multi)', 'Deselect', 'Deselect (multi)'];
    if (selectedNode.isLeaf) {
        choices[0] += ' (is leaf)';
        choices[1] += ' (is leaf)';
    } else {
        let expanded = await selectedNode.isExpanded();
        if (expanded) {
            choices[0] += ' (is expanded)';
        } else {
            choices[1] += ' (is collapsed)';
        }
    }
    let parent = await selectedNode.getParent();
    if (parent) {
        choices.push('Get Parent');
    }
    let children = await selectedNode.getChildren();
    children.forEach(child => choices.push(child.label));
    let choice = await vscode.window.showQuickPick(choices);
    let nextNode: azdata.objectexplorer.ObjectExplorerNode = undefined;
    if (choice === choices[0]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Expanded);
    } else if (choice === choices[1]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Collapsed);
    } else if (choice === choices[2]) {
        selectedNode.setSelected(true);
    } else if (choice === choices[3]) {
        selectedNode.setSelected(true, false);
    } else if (choice === choices[4]) {
        selectedNode.setSelected(false);
    } else if (choice === choices[5]) {
        selectedNode.setSelected(false, true);
    } else if (choice === 'Get Parent') {
        nextNode = parent;
    } else {
        let childNode = children.find(child => child.label === choice);
        nextNode = childNode;
    }
    if (nextNode) {
        let updatedNode = await azdata.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    azdata.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>建議的 API

我們新增了建議的 API，允許延伸模組在對話方塊、精靈和文件索引標籤中顯示自訂 UI，以及其他功能。 如需進一步說明，請參閱[建議的 API 類型檔案](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/azdata.proposed.d.ts)，但請注意，這些 API 隨時可能會變更。 您可以在 ["sqlservices" 範例延伸模組](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices)中，找到如何使用其中一些 API 的範例。


