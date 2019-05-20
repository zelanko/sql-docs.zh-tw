---
title: 針對 Reporting Services 報表的資料擷取問題進行疑難排解 | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: 7680946a-1660-4b59-a03a-c4d474cd8ed3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 86f1b8bda63cf8e6436e0dd3d5823fdada53a9f3
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65574431"
---
# <a name="troubleshoot-data-retrieval-issues-with-reporting-services-reports"></a>搭配 Reporting Services 報表為資料擷取問題疑難排解
在報表處理期間，第一個步驟是執行資料集查詢以擷取各資料集的報表資料。 在本機預覽報表時，您的資料來源連接和認證必須使用足夠的權限，才能將資料擷取到電腦上。 在報表伺服器上執行報表時，資料來源連接和認證也必須使用足夠的權限，才能將資料擷取到報表伺服器上。 您可以使用本主題來協助疑難排解有關報表資料擷取的問題。   
  
## <a name="i-cannot-create-a-connection-to-a-data-source"></a>無法與資料來源建立連接  
如果您在建立資料來源時執行資料集查詢或預覽報表，可能會收到下列訊息：無法與資料來源 `<data source name>`建立連接。   
    
### <a name="data-source-is-not-available"></a>資料來源無法使用。  
資料來源已離線，或者因其他原因而無法使用。   
  
確定您擁有資料來源的存取權限，而且該資料來源可以使用。 例如，使用 SQL Server Management Studio 連接資料來源。 針對關聯式資料庫和多維度資料庫，使用 [連接屬性] 對話方塊上的 [測試] 按鈕，確認資料來源的連接和權限。   
  
### <a name="data-source-credentials-are-not-valid"></a>資料來源認證無效。  
您用於連接資料來源的認證權限不足，無法擷取在查詢中指定的資料。  
  
確認您所使用的認證正確。 例如，您可能具有可以從資料表或檢視擷取資料的權限，但該權限不適用於特定資料行；或者您沒有足夠的權限來執行擴展檢視的預存程序。   
  
> [!NOTE]  
> 為了預覽報表而用於擷取資料的權限，可能不同於在報表發行至報表伺服器後，用於擷取資料的權限。   
  
### <a name="not-a-valid-password"></a>密碼無效  
資料來源若包含提示認證或是指定在連接字串中的認證，密碼字元會傳送到基礎資料來源驅動程式。 如果密碼或字串包含標點符號之類的特殊字元，某些資料來源驅動程式可能無法驗證特殊字元。   
  
確認密碼不包含特殊字元。 如果無法變更此密碼，請與資料庫管理員合作，將適當的認證儲存在本機以及伺服器上，當做系統 ODBC 資料來源名稱 (DSN) 的一部分。 如需詳細資訊，請參閱 MSDN 上 .NET Framework SDK 文件集中的＜OdbcConnection.ConnectionString＞。   
  
> [!NOTE]  
>建議您不要在連接字串中加入登入資訊，例如密碼。 報表設計師會在您可用來輸入認證的 [資料來源屬性] 或 [共用資料來源屬性] 對話方塊上提供 [認證] 頁面。 這些認證都加上保護，儲存在報表撰寫電腦上。  
  
## <a name="why-do-i-see-no-data-when-i-run-my-query-in-the-query-designer"></a>在查詢設計工具中執行查詢時，為什麼看不到資料？  
當您建立資料集之後，資料集欄位集合會出現在 [報表資料] 窗格中。 有時候，資料集欄位集合不會如預期顯示。   
  
### <a name="import-query-does-not-import-calculated-fields"></a>匯入查詢不會匯入導出欄位  
  
導出欄位雖然儲存在報表定義中，但是當您從其他報表匯入資料集查詢時卻不會包含導出欄位。 從其他報表匯入查詢以建立資料集之後，只有由資料集查詢指定的欄位會出現在 [報表資料] 窗格中。   
  
若要在 [報表資料] 窗格中檢視導出欄位，您必須為使用導出欄位的每個報表，定義導出欄位。   
  
### <a name="some-data-providers-do-not-support-automatic-population-of-the-dataset-field-collection"></a>某些資料提供者不支援資料集欄位集合的自動擴展  
當您在 [資料集屬性] 對話方塊中定義查詢並關閉對話方塊之後，資料集欄位集合通常會顯示在 [報表資料] 窗格中。 針對某些資料來源，資料集欄位集合不會自動擴展。   
  
若要擴展資料集欄位集合，請執行下列動作：  
* 請確定您擁有從資料庫中擷取欄位資訊的權限。 針對某些資料來源，您可能擁有存取資料來源的權限，但是沒有存取資料表或資料行的權限。 您可能擁有存取檢視的權限，但對於建立檢視的預存程序，卻沒有執行權限。 若要驗證您對資料庫中特定資料表或資料行的存取權，請使用您用於報表的相同權限，在 SQL Server Management Studio 等個別應用程式中確認查詢結果。 如果您無法看到想要的查詢結果，請與系統管理員一起調整您對資料的權限。   
* 在 [資料集屬性] 對話方塊的 [查詢] 窗格中執行查詢。 如需詳細資訊，請參閱[報表資料集 (報表產生器 3.0 及 SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)。  
* 手動加入欄位。 如需詳細資訊，請參閱 [如何：加入、編輯、重新整理報表資料窗格中的欄位 (報表產生器 3.0 及 SSRS)](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。   
  
## <a name="see-also"></a>另請參閱  
[錯誤和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]



