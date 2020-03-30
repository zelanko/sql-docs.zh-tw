---
title: 比較複寫資料表的差異 (複寫 SP)
description: 使用複寫預存程序來比較「發行者」和「訂閱者」複寫資料表之間的差異。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- tablediff utility
- comparing replicated tables
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6130acf6a503f3a803978b7db5a9a23b9918a3c7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286863"
---
# <a name="compare-differences-between-replicated-tables-replication-programming"></a>比較複寫資料表的差異 (複寫程式設計)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  發行項驗證可用來判斷「發行者」和「訂閱者」端資料表發行項的發行資料是否互異，若有則可能代表無法聚合。 如需詳細資訊，請參閱[驗證複寫的資料](../../../relational-databases/replication/validate-data-at-the-subscriber.md)。 不過，驗證只會傳回通過或失敗資訊，而不會針對來源及目的地資料表之間的差異提供任何相關資訊。 **tablediff** 命令提示字元公用程式會傳回兩個資料表之間差異的詳細資訊，甚至可能產生 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼，將訂閱向發行者端的資料聚合。  
  
> [!NOTE]  
>  只有 **伺服器支援** tablediff [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 公用程式。  
  
### <a name="to-compare-replicated-tables-for-differences-using-tablediff"></a>若要使用 tablediff 比較複寫資料表的差異  
  
1.  從複寫拓撲中任何伺服器的命令提示字元執行 [tablediff Utility](../../../tools/tablediff-utility.md)。 指定下列參數：  
  
    -   **-sourceserver** - 已知其上資料正確的伺服器名稱，通常是「發行者」端。  
  
    -   **-sourcedatabase** - 包含正確資料之資料庫的名稱。  
  
    -   **-sourcetable** - 所比較發行項之來源資料表的名稱。  
  
    -   (選擇性) **-sourceschema** - 來源資料表的結構描述擁有者 (若非預設的結構描述)。  
  
    -   (選擇性) 在使用「SQL Server 驗證」連接到「發行者」時，使用 **-sourceuser** 和 **-sourcepassword** 。  
  
        > [!IMPORTANT]  
        >  盡可能使用 Windows 驗證。 如果必須使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」，請提示使用者在執行階段輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
    -   **-destinationserver** - 所比較資料所在伺服器的名稱，通常是「訂閱者」。  
  
    -   **-destinationdatabase** - 所比較資料庫的名稱。  
  
    -   **-destinationtable** - 所比較資料表的名稱。  
  
    -   (選擇性) **-destinationschema** - 目的地資料表的結構描述擁有者 (若非預設的結構描述)。  
  
    -   (選擇性) 在使用「 **驗證」連接到「訂閱者」時，使用** -destinationuser **和** -destinationpassword [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
        > [!IMPORTANT]  
        >  盡可能使用 Windows 驗證。 如果必須使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」，請提示使用者在執行階段輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
    -   (選擇性) 使用 **-c** 可執行資料行層級比較。  
  
    -   (選擇性) 使用 **-q** 可執行僅限列數和結構描述的快速比較。  
  
    -   (選擇性) 針對 **-o** 指定檔案名稱和路徑，以將結果輸出至檔案。  
  
    -   (選擇性) 指定訂閱資料庫中的資料表，以在其中插入 **-et**的結果。 如果該資料表已存在，請指定 **-dt** 先將該資料表卸除。  
  
    -   (選擇性) 使用 **-f** 可產生 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 檔案，以修正「訂閱者」端的資料，使其符合「發行者」端的資料。 使用 **-df** 可指定每個檔案中的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式數目。  
  
    -   (選擇性) 使用 **-rc** 和 **-ri** 可指定重試作業的次數和重試間隔。  
  
    -   (選擇性) 使用 **-strict** 可在來源和目的地資料表之間強制執行嚴格的結構描述比較。  
  
## <a name="see-also"></a>另請參閱  
 [驗證訂閱者端的資料](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
