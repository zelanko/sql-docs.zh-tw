---
title: 具名管道屬性
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 923f84ccc98837892d144a07ce71238c877ca5b6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75306447"
---
# <a name="named-pipes-properties"></a>具名管道屬性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  使用具名管道通訊協定時，您可以使用 [具名管道屬性]  對話方塊上的 [通訊協定]  頁面，以檢視或變更 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽的具名管道。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須重新啟動，才能啟用或停用通訊協定或變更具名管道。  
  
## <a name="options"></a>選項。  
 **已啟用**  
 可能的值為 [是]  和 [否]  。  
  
 **管道名稱**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽的具名管道。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對於預設執行個體會接聽： `\\.\pipe\sql\query` ，而對於具名執行個體會接聽： `\\.\pipe\MSSQL$<instancename>\sql\query` 。 此欄位最長不可超過 2047 個字元。  
  
## <a name="creating-an-alternate-named-pipe"></a>建立替代具名管道  
 若要變更具名管道，請在 [具名管道]  方塊中輸入新的管道名稱，然後停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，之後再重新啟動。 因為已知 **sql\query** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的具名管道，所以變更管道有助於降低遭惡意程式攻擊的風險。  
  
### <a name="example"></a>範例  
 輸入 **\\\\.\pipe\unit\app** 以接聽 **unit\app** 管道。  
  
 輸入 **\\\\.\pipe\acct** 以接聽 **acct** 管道。  
  
## <a name="see-also"></a>另請參閱  
 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [選擇網路通訊協定](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [使用具名管道建立有效的連接字串](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  
