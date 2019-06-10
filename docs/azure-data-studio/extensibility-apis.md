---
title: 擴充性 API
titleSuffix: Azure Data Studio
description: 了解擴充性 Api 適用於 Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 3cde890f16e14866238f24e5d8a6bd52efdc9ecc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782423"
---
# <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 擴充性 Api

[!INCLUDE[name-sos](../includes/name-sos.md)] 提供擴充功能可以用來與 Azure Data Studio，例如 [物件總管] 中的其他部分互動的 API。 這些 Api 都是從[ `src/sql/sqlops.d.ts` ](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.d.ts)檔案，並如下所述。

## <a name="connection-management"></a>連接管理
`sqlops.connection`

### <a name="top-level-functions"></a>最上層函式

- `getCurrentConnection(): Thenable<sqlops.connection.Connection>` 取得目前使用中編輯器或物件總管 中選取項目為基礎的連接。

- `getActiveConnections(): Thenable<sqlops.connection.Connection[]>` 取得一份作用中的所有使用者的連線。 如果沒有這類的連接，則傳回空的清單。

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` 取得字典，其中包含與連接相關聯的認證。 這些會否則選項字典下的一部分傳回`sqlops.connection.Connection`物件，但取得從該物件中移除。 

### `Connection`
- `options: { [name: string]: string }` 字典的連線選項
- `providerName: string` 連線提供者的名稱 （例如："MSSQL")
- `connectionId: string` 連接的唯一識別碼

### <a name="example-code"></a>範例程式碼
```
> let connection = sqlops.connection.getCurrentConnection();
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
> let credentials = sqlops.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>物件總管

`sqlops.objectexplorer`


### <a name="top-level-functions"></a>最上層函式
- `getNode(connectionId: string, nodePath?: string): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 取得對應至給定的連接和路徑的物件總管 節點。 如果未不指定任何路徑，則它會傳回所指定連接的最上層節點。 如果並沒有節點在指定的路徑，它會傳回`undefined`。 注意:`nodePath`物件由 SQL 工具服務後端所產生，而且很難以手動方式建構。 未來的 API 增強功能可讓您能夠根據您提供相關的節點，例如名稱、 類型和結構描述的中繼資料的節點。

- `getActiveConnectionNodes(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 取得所有作用中的物件總管 連接節點。

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` 尋找所有符合指定之中繼資料的物件總管 節點。 `schema`， `database`，並`parentObjectNames`引數應`undefined`時不適用。 `parentObjectNames` 是一份非資料庫的父物件，從最高到最低的層級，在 [物件總管] 中，所需的物件正在進行中。 例如，當使用連接識別碼搜尋的資料行所屬資料表 」 schema1.table1 」 和資料庫"database1"的"column1" `connectionId`，呼叫`findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`。 另請參閱[的預設 Azure Data Studio 支援的類型清單](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API)這個 API 呼叫。

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` 底下的節點有連接的識別碼

- `nodePath: string` 節點路徑，與用於呼叫`getNode`函式。

- `nodeType: string` 字串，表示節點的類型

- `nodeSubType: string` 字串，表示節點的子類型

- `nodeStatus: string` 字串，表示節點的狀態

- `label: string` 節點的標籤會出現在 [物件總管]

- `isLeaf: boolean` 節點是否為分葉節點，並因此並沒有子系

- `metadata: sqlops.ObjectMetadata` 描述此節點所表示之物件的中繼資料

- `errorMessage: string` 顯示節點是否處於錯誤狀態訊息

- `isExpanded(): Thenable<boolean>` 在 物件總管節點目前是否已展開

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` 設定節點為展開或摺疊。 如果狀態設定為 None 時，節點將不會變更。

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` 設定是否已選取的節點。 如果`clearOtherSelections`是 true，則清除任何其他選取項目，建立新的選取範圍時。 如果為 false，將保留任何現有的選取項目。 `clearOtherSelections` 預設值為 true 時`selected`時，則為 true 和 false`selected`為 false。

- `getChildren(): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` 取得所有子節點的此節點。 如果沒有任何子系，則傳回空的清單。

- `getParent(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` 取得此節點的父節點。 如果沒有父代，傳回未定義。

### <a name="example-code"></a>範例程式碼

```cs
private async interactWithOENode(selectedNode: sqlops.objectexplorer.ObjectExplorerNode): Promise<void> {
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
    let nextNode: sqlops.objectexplorer.ObjectExplorerNode = undefined;
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
        let updatedNode = await sqlops.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    sqlops.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>建議的 Api

我們已新增建議的 Api，以允許在對話方塊、 精靈和其他功能方面的文件索引標籤，顯示自訂 UI 的延伸模組。 請參閱[提議的 API 類型檔案](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.proposed.d.ts)如需詳細的文件，不過請注意，這些 API 可能會有所變更，在任何時間。 範例，示範如何使用這些 Api 的一些可在["sqlservices 」 範例延伸模組](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices)。


