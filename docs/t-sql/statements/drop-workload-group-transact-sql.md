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
ms.openlocfilehash: 6e75e84884bca1fef4d42a64056e2ef38111e6db
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75952334"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>按一下產品！

在下列資料列中，按一下您感興趣的產品名稱。 視您所按下的產品而定，此點選會在本網頁的這裡顯示不同的內容。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[SQL Database<br />受控執行個體](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server 和 SQL Database 受控執行個體

卸除現有使用者定義的資源管理員工作負載群組。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>語法

```
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>引數

*group_name* 是現有使用者定義之工作負載群組的名稱。

## <a name="remarks"></a>備註

在資源管理員的內部或預設群組上，不允許使用 DROP WORKLOAD GROUP 陳述式。

當您要執行 DDL 陳述式時，建議您先熟悉資源管理員的狀態。 如需詳細資訊，請參閱 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)。

如果工作負載群組包含使用中工作階段，當呼叫 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式以套用變更時，卸除工作負載群組或將工作負載群組移到不同的資源集區將會失敗。 若要避免這個問題，您可以採取下列其中一個動作：

- 等到受影響之群組的所有工作階段已經中斷連接後，重新執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。

- 在受影響的群組中，使用 KILL 命令明確地停止工作階段，然後重新執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。

- 重新啟動伺服器。 重新啟動程序完成後，將不會建立已經刪除的群組，而且已經移動的群組將會使用新的資源集區指派。

- 在您已經發出 DROP WORKLOAD GROUP 陳述式但決定您不要明確地停止工作階段以套用變更的實例中，您可以使用您發出 DROP 陳述式前的相同名稱重新建立群組，然後將該群組移到原始的資源集區。 若要套用變更，請執行 ALTER RESOURCE GOVERNOR RECONFIGURE 陳述式。

## <a name="permissions"></a>權限

需要 CONTROL SERVER 權限。

## <a name="examples"></a>範例

下列範例會卸除名稱為 `adhoc` 的工作負載群組。

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>另請參閱

- [資源管理員](../../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)||[SQL Database<br />受控執行個體](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* Azure Synapse<br />Analytics \*_** &nbsp;||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics (預覽)

卸除工作負載群組。  一旦陳述式完成，設定就會生效。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>語法

```
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
