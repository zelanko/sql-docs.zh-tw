---
title: 設定或變更伺服器定序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4501bc77a28746de3b0ce97b7b619889093650d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918574"
---
# <a name="set-or-change-the-server-collation"></a>設定或變更伺服器定序
  對於與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體一起安裝的所有系統資料庫，以及任何新建的使用者資料庫而言，伺服器定序會當做預設定序。 伺服器定序是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間指定。 如需詳細資訊，請參閱 [Collation and Unicode Support](collation-and-unicode-support.md)。  
  
## <a name="changing-the-server-collation"></a>變更伺服器定序  
 變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的預設定序是相當複雜的作業，需要執行下列步驟：  
  
-   確定已備妥重新建立使用者資料庫以及所有內含物件所需的所有資訊或指令碼。  
  
-   使用 [bcp Utility](../../tools/bcp-utility.md)這類工具來匯出所有資料。 如需詳細資訊，請參閱[資料的大量匯入及匯出 &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
-   卸除所有使用者資料庫。  
  
-   重建 master 資料庫，以使用 **setup** 命令的 SQLCOLLATION 屬性來指定新定序。 例如：  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName   
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]   
    /SQLCOLLATION=CollationName  
    ```  
  
     如需詳細資訊，請參閱 [重建系統資料庫](../databases/system-databases.md)。  
  
-   建立所有資料庫以及所有內含物件。  
  
-   匯入所有資料。  
  
> [!NOTE]  
>  您可以不變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的預設定序，而是針對每個建立的新資料庫指定預設定序。  
  
## <a name="see-also"></a>另請參閱  
 [Collation and Unicode Support](collation-and-unicode-support.md)   
 [設定或變更資料庫定序](set-or-change-the-database-collation.md)   
 [設定或變更資料行定序](set-or-change-the-column-collation.md)   
 [重建系統資料庫](../databases/system-databases.md)  
  
  
