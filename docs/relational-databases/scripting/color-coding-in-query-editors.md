---
title: 查詢編輯器中的色彩編碼 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], color coding
- color coding [Query Editor]
ms.assetid: 802882dc-c997-4e3f-8a01-994bb43169ae
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 25392403e587451d44a000ab78b904626f4f0dd7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47852537"
---
# <a name="color-coding-in-query-editors"></a>查詢編輯器中的色彩編碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  在程式碼編輯器中輸入的文字會指派至類別目錄；每一個類別目錄都會以色彩識別。 這些色彩可協助您快速地找到程式碼中的文字。 例如，註解會以深綠色突顯出來。 下表將列出最常見的色彩。 您可以檢視色彩及其類別目錄的完整清單，也可以使用 [工具] 和 [選項] 功能表來設定自訂的色彩配置。 如需如何變更預設色彩的詳細資訊，請參閱[變更字型色彩、大小與樣式](../../relational-databases/scripting/change-font-color-size-and-style.md)。  
  
## <a name="default-code-colors"></a>預設程式碼色彩  
  
|Color|類別目錄|  
|-----------|--------------|  
|紅色|SQL 字串|  
|深綠色|註解|  
|銀底黑色|SQLCMD 命令|  
|桃紅色|系統功能|  
|綠色|系統資料表、檢視或資料表值函式。 此外，還包括系統結構描述 sys 與 INFORMATION_SCHEMA。|  
|藍色|關鍵字|  
|藍綠色|行號或範本參數|  
|暗紅色|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序|  
|深灰色|運算子|  
  
## <a name="status-bar"></a>狀態列  
 您可以在 [物件總管] 中設定已註冊的伺服器或 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 伺服器，讓 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器] 狀態列中顯示不同的色彩。 這可協助您在同時開啟多個視窗時，識別每個編輯器視窗所連接的伺服器。 如需設定狀態列色彩的詳細資訊，請參閱[狀態列 &#40;Database Engine 查詢編輯器&#41;](../../relational-databases/scripting/status-bar-database-engine-query-editor.md)。  
  
 某些類型的編輯器不會顯示狀態列，或不支援多種色彩。  
  
  
