---
title: 查詢編輯器中的色彩編碼
description: 了解如何為文字類別進行色彩編碼，從而協助更輕鬆地尋找特定文字，以及如何設定自訂色彩配置。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], color coding
- color coding [Query Editor]
ms.assetid: 802882dc-c997-4e3f-8a01-994bb43169ae
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d83afc075542a3dce2bfeb13272194efc661f7f9
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039104"
---
# <a name="color-coding-in-query-editors"></a>查詢編輯器中的色彩編碼

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

在程式碼編輯器中輸入的文字會指派至類別目錄；每一個類別目錄都會以色彩識別。 這些色彩可協助您快速地找到程式碼中的文字。 例如，註解會以深綠色突顯出來。 下表將列出最常見的色彩。 您可以檢視色彩及其類別目錄的完整清單，也可以使用 [工具] 和 [選項] 功能表來設定自訂的色彩配置。 如需如何變更預設色彩的詳細資訊，請參閱 [變更字型色彩、大小與樣式](./change-font-color-size-and-style.md)。  
  
## <a name="default-code-colors"></a>預設程式碼色彩  
  
|Color|類別|  
|-----------|--------------|  
|紅色|SQL 字串|  
|深綠色|註解|  
|銀底黑色|SQLCMD 命令|  
|桃紅色|系統函式|  
|綠色|系統資料表、檢視或資料表值函式。 此外，還包括系統結構描述 sys 與 INFORMATION_SCHEMA。|  
|藍色|關鍵字|  
|藍綠色|行號或範本參數|  
|暗紅色|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序|  
|深灰色|操作員|  
  
## <a name="status-bar"></a>狀態列  
 您可以在 [物件總管] 中設定已註冊的伺服器或 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 伺服器，讓 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器] 狀態列中顯示不同的色彩。 這可協助您在同時開啟多個視窗時，識別每個編輯器視窗所連接的伺服器。 如需設定狀態列色彩的詳細資訊，請參閱[狀態列 &#40;Database Engine 查詢編輯器&#41;](./status-bar-database-engine-query-editor.md)。  
  
 某些類型的編輯器不會顯示狀態列，或不支援多種色彩。  
  
