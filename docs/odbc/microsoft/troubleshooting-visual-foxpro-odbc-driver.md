---
description: 疑難排解 (Visual FoxPro ODBC Driver)
title: 疑難排解 (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73f98f66a09b0ff17987186103b38643047f1762
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471431"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>疑難排解 (Visual FoxPro ODBC Driver)
下列各節討論如何改善效能，並解決使用 Visual FoxPro ODBC 驅動程式時可能遇到的問題。  
  
## <a name="accessing-parameterized-views"></a>存取參數化視圖  
 您無法使用驅動程式存取 Visual FoxPro 資料庫中的參數化視圖。 參數化視圖會在 view 的 SQL **SELECT** 語句中建立 WHERE 子句，以將下載的記錄限制為符合 WHERE 子句條件（使用針對參數所提供的值建立）的記錄。 因為驅動程式不支援將參數傳遞給視圖，所以嘗試使用驅動程式存取參數化視圖會失敗。  
  
 您可以在執行時間提供參數值，或以程式設計的方式傳遞給視圖。  
  
## <a name="accessing-remote-views"></a>存取遠端查看  
 您無法使用驅動程式存取 Visual FoxPro 資料庫中的遠端資料視圖。 遠端視圖是指存取非 FoxPro 資料或 FoxPro 和非 FoxPro 資料組合的視圖。 若要存取遠端視圖，請使用 Visual FoxPro。  
  
## <a name="deleting-records"></a>刪除記錄  
 您可以使用驅動程式標示要刪除的記錄，但無法從資料庫中永久移除記錄。 若要永久移除資料表中的記錄，請使用 Visual FoxPro。  
  
## <a name="increasing-performance-using-background-fetching"></a>使用背景提取來提高效能  
 您可以使用驅動程式的「背景提取」功能來改善大型提取的效能。 背景提取使用不同的執行緒來提取從特定資料來源要求的資料。  
  
 您可以使用下列其中一種方式，對資料來源採用背景提取：  
  
-   在 [ [ODBC Visual FoxPro 安裝程式] 對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)上，勾選 [**在背景中提取資料**] 核取方塊。  
  
-   在連接字串中使用 BackgroundFetch attribute 關鍵字。  
  
 如需連接字串屬性關鍵字的詳細資訊，請參閱 [使用連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
## <a name="updating-multitiered-views"></a>更新各層的觀點  
 多層式視圖是以一或多個視圖為基礎，而不是基表上的視圖。 當您在多層式視圖中更新資料時，更新只會從一個層級向下移至最上層視圖所依據的視圖;基表未更新。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>在預存程式中使用資料定義語言 (DDL)   
 您無法在 Visual FoxPro 預存程式中使用 DDL，例如 CREATE TABLE 或 ALTER TABLE。  
  
 如需有關您可以在預存程式中使用之語言的詳細資訊，請參閱 [支援規則、觸發程式、預設值和預存程式](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)。  
  
## <a name="using-positioned-updates"></a>使用定點更新  
 驅動程式不支援定點更新。 使用 SQL WHERE 子句來識別您想要更新的資料列。  
  
## <a name="using-the-set-ansi-command"></a>使用 SET ANSI 命令  
 如果您是 Visual FoxPro 開發人員，您應該注意到驅動程式的 SET ANSI 預設設定是 ON，相較于 Visual FoxPro 的預設設定為 OFF。 SET ANSI 的預設 ON 設定可讓 Visual FoxPro 資料來源與其他通常執行精確比較的 ODBC 資料來源一致。 您可以變更預設設定。 如需詳細資訊，請參閱 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)。
