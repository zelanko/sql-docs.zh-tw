---
title: "專案設定 (Azure SQL DB) (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d56834df6e86edcf9821781faa1144afaa2d8d6e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>專案設定 (Azure SQL DB) (MySQLToSQL)
SQL Azure 專案設定可讓您設定 新增連接對話方塊中，而且也允許 活動訊號機制實作 SQL Azure 連接中的 SQL Azure 資料庫尾碼。  
  
SQL Azure 窗格位於**專案設定**和**預設專案設定**對話方塊。  
  
-   使用 [專案設定] 對話方塊，設定目前專案的組態選項。 若要存取 SQL Azure 的設定，在**工具**功能表上，選取**專案設定**，按一下 **一般**底部的左的窗格，然後選取**SQL Azure**。  
  
-   您可以使用預設專案設定 對話方塊來設定所有專案的組態選項。 若要存取 SQL Azure 的設定，在**工具**功能表上，選取**DefaultProject 設定**，選取從 SQL Azure 移轉專案類型**移轉的目標版本**存取 SQL Azure 窗格中的設定，請按一下下拉式清單**一般**底部的左的窗格，然後選取**SQL Azure**。  
  
## <a name="options"></a>選項  
  
## <a name="connectivity"></a>連接性  
**活動訊號間隔時間**  
  
指定要用於活動訊號機制，以保持存留在 SQL Azure 連接時間間隔 ' 分鐘： 秒數的格式。  
  
**預設值**:' 4:45 '  
  
應該指定的值在我： ss 的格式 (例如，' 4:45 '或' 0:50 ')。  
  
**SQL Azure 伺服器後置詞**  
  
指定的 SQL Azure 伺服器尾碼  
  
**預設值**: '.database.windows.net'。  
  

