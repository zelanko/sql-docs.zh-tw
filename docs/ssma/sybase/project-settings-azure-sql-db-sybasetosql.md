---
title: 專案設定 (Azure SQL DB) (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: afce63dc96d2e7d5d95f6a685e625987cd25c7cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>專案設定 (Azure SQL DB) (SybaseToSQL)
Azure SQL 資料庫專案設定可讓您設定 新增連接對話方塊中，而且也允許 活動訊號機制實作 Azure SQL DB 連接中的 Azure SQL DB 資料庫尾碼。  
  
Azure SQL DB 窗格位於**專案設定**和**預設專案設定**對話方塊。  
  
-   使用 [專案設定] 對話方塊，設定目前專案的組態選項。 若要存取 Azure SQL DB 設定，在**工具**功能表上，選取**專案設定**，按一下 **一般**底部的左的窗格，然後選取**Azure SQL DB**。  
  
-   您可以使用預設專案設定 對話方塊來設定所有專案的組態選項。 若要存取 Azure SQL DB 設定，在**工具**功能表上，選取**DefaultProject 設定**，按一下 **一般**底部的左的窗格，然後選取**Azure SQL DB**。  
  
## <a name="connectivity"></a>連接性  
**活動訊號間隔時間**  
  
指定要用於活動訊號機制，以保持 Azure SQL DB 連線運作中的時間間隔 ' 分鐘： 秒數的格式。  
  
**預設值**:' 4:45 '  
  
應該指定的值在我： ss 的格式 (例如，' 4:45 '或' 0:50 ')。  
  
**Azure SQL DB 伺服器後置詞**  
  
指定 Azure SQL DB 伺服器後置詞  
  
**預設值**: '.database.windows.net'。  
  
