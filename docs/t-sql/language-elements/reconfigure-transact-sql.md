---
title: RECONFIGURE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/20/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RECONFIGURE
- RECONFIGURE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- reconfiguring configuration options
- configuration options [SQL Server], reconfiguring
- updating configuration options
- RECONFIGURE, RECONFIGURE statement
- RECONFIGURE
- RECONFIGURE, WITH OVERRIDE statement
ms.assetid: 2e6e4eeb-b70b-4f45-a253-28ac4e595d75
caps.latest.revision: "50"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 432e5157969a10f36273db3bbd8990fa9e332b68
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新目前設定的值 ( **config_value**中的資料行**sp_configure**結果集) 的組態選項，以變更**sp_configure**系統預存程序。 因為某些設定選項需要伺服器停止再重新啟動才能更新目前執行中的值，RECONFIGURE 永遠不會更新目前執行中的值 ( **run_value**中的資料行**sp_configure**結果集) 已變更的組態值。    
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>語法    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>引數    
 RECONFIGURE    
 指定如果組態設定不需要停止再重新啟動伺服器，便應該更新目前在執行的值。 RECONFIGURE 也會檢查新的組態值，可能是無效的值 (例如，排序次序值，不存在於**syscharsets**) 或非建議的值。 當使用不需要停止再重新啟動伺服器的組態選項時，在指定 RECONFIGURE 之後，組態選項目前在執行的值和目前已設定的值應該相同。    
    
 WITH OVERRIDE    
 停用檢查 （不是有效的值或非建議值） 的組態值**復原間隔**進階組態選項。    
    
 幾乎所有組態選項可以使用 WITH OVERRIDE 選項，但是有些嚴重錯誤仍會避免重新都設定。 例如，**最小伺服器記憶體**無法設定組態選項的值中指定的值大於**最大伺服器記憶體**組態選項。
      
## <a name="remarks"></a>備註    
 **sp_configure**不接受新的組態選項值，超出文件的有效範圍，每個組態選項。    
    
 在明確或隱含的交易中，不允許使用 RECONFIGURE。 當您同時重新設定數個選項時，若有任何重新設定作業失敗，則所有重新設定作業都不會生效。    
    
 當重新設定資源管理員，請參閱 RECONFIGURE 選項[ALTER RESOURCE GOVERNOR &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Permissions    
 RECONFIGURE 權限預設給 ALTER SETTINGS 權限的被授與者。 **Sysadmin**和**serveradmin**固定的伺服器角色會隱含地保留這個權限。    
    
## <a name="examples"></a>範例    
 下列範例將 `recovery interval` 組態選項的上限設為 `75` 分鐘，並利用 `RECONFIGURE WITH OVERRIDE` 來安裝它。 不建議您使用超出 60 分鐘的復原間隔，依預設，不會接受這個值。 不過，由於指定了 `WITH OVERRIDE` 選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不會檢查指定的值 (`90`) 是否為 `recovery interval` 組態選項的有效值。    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>另請參閱    
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  
