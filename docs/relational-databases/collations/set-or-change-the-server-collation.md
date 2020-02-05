---
title: 設定或變更伺服器定序 | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: carlrab
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 019c62424398b05dfaa6efe2f91ab4c08b333cd2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "74901919"
---
# <a name="set-or-change-the-server-collation"></a>設定或變更伺服器定序

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  對於與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體一起安裝的所有系統資料庫，以及任何新建的使用者資料庫而言，伺服器定序會當做預設定序。 您應該仔細選擇伺服器層級定序，因為它會影響：
 - `=`、`JOIN`、`ORDER BY` 及比較文字資料之其他運算子的排序和比較規則。
 - 系統檢視表中 `CHAR`、`VARCHAR`、`NCHAR` 和 `NVARCHAR` 資料行以及系統函式和 TempDB (例如暫存資料表) 中物件的定序。
 - 變數、資料指標和 `GOTO` 標籤的名稱。 如果伺服器層級定序區分大小寫，變數 @pi 和 @PI 會視為不同的變數；如果伺服器層級定序不區分大小寫，則會視為相同的變數。
  
## <a name="setting-the-server-collation-in-sql-server"></a>設定 SQL Server 中的伺服器定序

  伺服器定序是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間指定。 預設伺服器層級定序為 **SQL_Latin1_General_CP1_CI_AS**。 無法將僅限 Unicode 定序指定為伺服器層級定序。 如需詳細資訊，請參閱 [Collation and Unicode Support](collation-and-unicode-support.md)。
  
## <a name="changing-the-server-collation-in-sql-server"></a>變更 SQL Server 中的伺服器定序

 變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的預設定序是相當複雜的作業，需要執行下列步驟：  
  
- 確定已備妥重新建立使用者資料庫以及所有內含物件所需的所有資訊或指令碼。  
  
- 使用 [bcp Utility](../../tools/bcp-utility.md)這類工具來匯出所有資料。 如需詳細資訊，請參閱[資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
- 卸除所有使用者資料庫。  
  
- 重建 master 資料庫，以使用 **setup** 命令的 SQLCOLLATION 屬性來指定新定序。 例如：  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]
    /SQLCOLLATION=CollationName  
    ```  
  
     如需詳細資訊，請參閱 [重建系統資料庫](../../relational-databases/databases/rebuild-system-databases.md)。  
  
- 建立所有資料庫以及所有內含物件。  
  
- 匯入所有資料。  
  
> [!NOTE]  
> 您可以不變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的預設定序，而是針對每個建立的新資料庫指定預設定序。  
  
## <a name="setting-the-server-collation-in-managed-instance"></a>設定受控執行個體中的伺服器定序
建立 Azure SQL 受控執行個體時，可指定執行個體中的伺服器層級定序，且稍後無法變更。 您可以在建立執行個體時，透過 [Azure 入口網站](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started#create-a-managed-instance)或 [PowerShell 和 Resource Manager 範本](https://docs.microsoft.com/azure/sql-database/scripts/sql-managed-instance-create-powershell-azure-resource-manager-template)來設定伺服器層級定序。 預設伺服器層級定序為 **SQL_Latin1_General_CP1_CI_AS**。 無法將僅限 Unicode 定序和新的 UTF-8 定序指定為伺服器層級定序。
如果您將資料庫從 SQL Server 移轉至受控執行個體，請使用 `SERVERPROPERTY(N'Collation')` 函式來檢查來源 SQL Server 中的伺服器定序，並建立符合您 SQL Server 定序的受控執行個體。 將資料庫從 SQL Server 移轉至伺服器層級定序不相符的受控執行個體，可能會導致查詢中出現數個未預期的錯誤。 您無法變更現有受控執行個體上的伺服器層級定序。

## <a name="see-also"></a>另請參閱

 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)   
 [設定或變更資料庫定序](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [設定或變更資料行定序](../../relational-databases/collations/set-or-change-the-column-collation.md)   
 [重建系統資料庫](../../relational-databases/databases/rebuild-system-databases.md)  
 
