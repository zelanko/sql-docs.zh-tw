---
title: 準備實作資料處理延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- interfaces [Reporting Services]
- data processing extensions [Reporting Services], implementing
ms.assetid: 698817e4-33da-4eb5-9407-4103e1c35247
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1eddc05cffbeb9fec926a47e4a9816b54434d48e
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2018
ms.locfileid: "40396238"
---
# <a name="preparing-to-implement-a-data-processing-extension"></a>準備實作資料處理延伸模組
  在您實作 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組之前，應該定義要實作的介面。 您可能會想要提供整組介面的延伸模組特定實作，或者您可能會直接將實作的集點放在子集上，例如 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 與 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> 介面，其中用戶端主要會與作為 **DataReader** 物件的結果集互動，而且將使用 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 資料處理延伸模組作為結果集與資料來源之間的橋樑。  
  
 您可以使用兩種方法之一來實作資料處理延伸模組：  
  
-   您的資料處理延伸模組類別可以實作 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 資料提供者介面，並選擇性地擴充 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 提供的資料處理延伸模組介面。  
  
-   您的資料處理延伸模組類別可以實作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 提供的資料處理延伸模組介面，並選擇性地擴充資料處理延伸模組介面。  
  
 如果您的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組不支援特定的屬性或方法，請將屬性或方法實作成無作業。 如果用戶端預期特定的行為，會擲回 **NotSupportedException** 例外狀況。  
  
> [!NOTE]  
>  屬性或方法的無作業實作，只適用於您選擇實作的那些介面之屬性和方法。 您選擇不實作的選擇性介面應該從資料處理延伸模組組件中排除。 如需有關介面是必要或選擇性的詳細資訊，請參閱本節稍後的資料表。  
  
## <a name="required-extension-functionality"></a>必要的擴充功能  
 每個 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組必須提供下列功能：  
  
-   開啟資料來源的連接。  
  
-   分析查詢並傳回結果集的欄位名稱清單。  
  
-   針對資料來源執行查詢並傳回資料列集。  
  
-   將單一值參數傳遞至查詢。  
  
-   反覆運算資料列集中的資料列並擷取資料。  
  
 每個資料處理延伸模組都可加以擴充以包括下列功能：  
  
-   分析查詢並傳回查詢所使用的參數名稱清單。  
  
-   分析查詢並傳回群組查詢所依據的欄位清單。  
  
-   分析查詢並傳回排序查詢所依據的欄位清單。  
  
-   提供使用者名稱與密碼以連接與連接字串無關的資料來源。  
  
-   反覆運算資料列集中的資料列，並擷取有關資料值的輔助中繼資料。  
  
-   在伺服器彙總資料。  
  
## <a name="available-extension-interfaces"></a>可用的延伸模組介面  
 下表描述可用的介面，以及實作是否為必要或為選擇性。  
  
|介面|描述|實作|  
|---------------|-----------------|--------------------|  
|IDbConnection|代表資料來源的唯一工作階段。 在用戶端/伺服器資料庫系統的情況下，此工作階段可能相當於伺服器的網路連接。|必要項|  
|IDbConnectionExtension|代表有關安全性與驗證之 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 資料處理延伸模組所實作的其他連接屬性。|選擇性|  
|IDbTransaction|表示本機交易。|必要項|  
|IDbTransactionExtension|代表可由 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 資料處理延伸模組所實作的其他交易屬性。|選擇性|  
|IDbCommand|代表當連接到資料來源時所使用的查詢或命令。|必要項|  
|IDbCommandAnalysis|代表分析查詢和傳回用於查詢的參數名稱清單的其他命令資訊。|選擇性|  
|IDataParameter|代表傳遞到命令或查詢的參數或名稱/值組。|必要項|  
|IDataParameterCollection|代表所有與命令或查詢相關的參數集合。|必要項|  
|IDataReader|提供一種方法，可順向且唯讀地讀取來自資料來源的資料流。|必要項|  
|IDataReaderExtension|提供方法來讀取一或多個藉由在資料來源處執行命令所取得的順向資料流之結果集。 這個介面會提供其他支援的欄位彙總。|選擇性|  
|IExtension|提供 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組的基底類別。 另外也可讓實作者包括當地語系化的延伸模組名稱，並將組態設定從組態檔傳遞到延伸模組。|必要項|  
  
 資料處理延伸模組介面會盡可能與 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 資料提供者介面、方法及屬性的子集相同。 如需有關實作完整 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 資料提供者的詳細資訊，請參閱＜[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 軟體開發套件 (SDK) 文件集中的＜實作 .NET Framework 資料提供者＞。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [實作資料處理延伸模組](implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
