---
title: DROP WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: d2bbbee44b7b50e5d25bda3b4d10c6123db6497b
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001153"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>按一下產品！

在下列資料列中，按一下您感興趣的產品名稱。 視您所按下的產品而定，此點選會在本網頁的這裡顯示不同的內容。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||
|---|---|---|
|**_\* SQL Server \*_** &nbsp;|[SQL Database<br />受控執行個體](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|
||||

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server 和 SQL Database 受控執行個體

[!INCLUDE [DROP WORKLOAD GROUP](../../includes/drop-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

||||
|---|---|---|
|[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)|**_\* SQL Database<br />受控執行個體 \*_** &nbsp;|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|
||||

&nbsp;

##  <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server 和 SQL Database 受控執行個體

[!INCLUDE [DROP WORKLOAD GROUP](../../includes/drop-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

||||
|---|---|---|
|[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)|[SQL Database<br />受控執行個體](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)| **_\* Azure Synapse<br />Analytics \*_** &nbsp;|
||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics (預覽)

卸除工作負載群組。  一旦陳述式完成，設定就會生效。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>語法

```syntaxsql
DROP WORKLOAD GROUP group_name  
```

## <a name="arguments"></a>引數

*group_name*  
現有使用者定義之工作負載群組的名稱。

## <a name="remarks"></a>備註

如果工作負載群組有分類器，就無法卸除該工作負載群組。  在卸除工作負載群組之前，請先卸除分類器。  如果有使用中的要求正在使用要卸除的工作負載群組中的資源，則會在其後封鎖該卸除工作負載陳述式。

## <a name="examples"></a>範例

使用下列程式碼範例，確定在卸除工作負載群組之前需要卸除哪些分類器。

```sql
SELECT c.name as classifier_name
      ,'DROP WORKLOAD CLASSIFIER '+c.name as drop_command
  FROM sys.workload_management_workload_classifiers c
  JOIN sys.workload_management_workload_groups g
    ON c.group_name = g.name
  WHERE g.name = 'wgXYZ' --change the filter to the workload being dropped
```

## <a name="permissions"></a>權限

需要 CONTROL DATABASE 權限

## <a name="see-also"></a>另請參閱

[CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)

::: moniker-end
