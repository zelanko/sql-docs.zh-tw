---
title: sp_polybase_leave_group & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 43f155de0eb81918d5129d404e7cd2f236957152
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037901"
---
# <a name="sppolybaseleavegroup-transact-sql"></a>sp_polybase_leave_group & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  移除 PolyBase 向外延展計算群組中的 SQL Server 執行個體。 
 
 SQL Server 執行個體必須具有[PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)安裝的功能。  PolyBase 可讓非 SQL Server 資料來源，例如 Hadoop 和 Azure blob 儲存體的整合。 另請參閱[sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="remarks"></a>備註  
 您只可以從群組移除計算節點。  
  
 執行預存程序之後, 重新啟動電腦上的 PolyBase 引擎和 PolyBase Data Movement Service。 若要確認在前端節點上執行下列 DMV: **sys.dm_exec_compute_nodes**。  
  
## <a name="example"></a>範例  
 此範例從 PolyBase 群組中移除目前的電腦。  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
