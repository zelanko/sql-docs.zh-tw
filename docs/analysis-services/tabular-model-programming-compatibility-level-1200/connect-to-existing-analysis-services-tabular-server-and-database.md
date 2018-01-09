---
title: "連接到現有的 Analysis Services 表格式伺服器和資料庫 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 05be704e-4ee4-4101-b5ce-96fdda18c639
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9f8282029d3f20075ed35b29e1af913a882075da
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>連接到現有的 Analysis Services 表格式伺服器和資料庫
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]在 SQL Server 2016 中，Analysis Services 管理物件 (AMO) 會包含可用來設定伺服器連接的數個命名空間。 本文說明如何建立伺服器連接的 Microsoft.AnalysisServices.Tabular 命名空間使用模型以及資料庫建立在 1200年或更高的相容性層級。 

若要連接到 Analysis Services 伺服器，您的程式碼必須具現化伺服器物件，然後在其上呼叫 Connect 方法。 一旦連接之後，伺服器物件的屬性會反映目前的 Analysis Services 執行個體的設定。 

下列類別可以用最上層的連線： 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

如您所見，兩個命名空間提供的伺服器和資料庫物件的連接： AMO 的原始 Microsoft.AnalysisServices 命名空間和新的 Microsoft.AnalysisServices.Tabular 命名空間為 TOM。

為什麼相同作業的兩個命名空間？ 答案就下游，其中物件階層會變成模式特定，而將模型樹狀結構由多維度或表格式中繼資料所組成的資料庫和模型層級。 若要將模型樹狀結構進行呼叫，這兩種模型類型提供的伺服器或資料庫物件。

> [!NOTE]  
>  使用模型定義和作業的中繼資料是完全不同的兩種模式。 藉由分隔成兩個不同的命名空間的資料定義語言 (DDL)，開發經驗已經過簡化透過只針對特定模型類型所需的 API 的呈現方式。 

雖然 DDL 不同，連線到伺服器都是相同模式、 版本和版本。 支援的伺服器和資料庫連接，透過其中一個命名空間可讓您撰寫泛型工具或指令碼，連接到任何 Analysis Services 執行個體或資料庫，而不需要知道何種類型的模型裝載在伺服器上。  

這種彈性說明的組件之間的相依性。 為了使下列資料庫層級 （例如，在表格式 1200年資料庫內的模型或 Cube、 維度或量值群組內的多維度或表格式 1050年-1103年資料庫） 的呼叫，AMO 會 TOM 上具有相依性。 

相反地，TOM 沒有相依性上 AMO。 雖然 TOM 無法用來瀏覽多維度中繼資料 (Cube)，AMO 可用於瀏覽多維度與表格式中繼資料。 

基於這個理由，您的專案設定的第一個步驟會需要將參考加入至所有的 AMO 組件。 請參閱[安裝參考及散發 TOM 用戶端程式庫](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)如需詳細資訊。 

> [!NOTE]  
>  伺服器和資料庫連線根據舊版 AMO 類別繼承自 MajorObject。 雖然表格式模型樹狀結構中不會使用主要和次要物件，此 MajorObject 類別是顯示為伺服器和資料庫物件，不論哪一個應用程式開發介面您使用來設定連線的基底類別。  

## <a name="code-example-server-connection"></a>程式碼範例： 伺服器連接 

以下是 C# 程式碼範例示範如何連接至本機 Analysis Services 執行個體，並列出其主控台視窗中的屬性。 

這個範例只會顯示部分內容的伺服器物件，但有可用的更多屬性，包括 ServerMode 和 DefaultCompatibilityLevel。  

```
using System; 
using Microsoft.AnalysisServices.Tabular; 

namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 


            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 

 
                Console.WriteLine("Connection established successfully."); 
                Console.WriteLine(); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.WriteLine("Server name:\t\t{0}", server.Name); 
                Console.WriteLine("Server product name:\t{0}", server.ProductName); 
                Console.WriteLine("Server product level:\t{0}", server.ProductLevel); 
                Console.WriteLine("Server version:\t\t{0}", server.Version); 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```
當您執行此程式時，輸出會顯示在主控台視窗中的伺服器物件上的屬性。 

## <a name="authentication-and-authorization"></a>驗證和授權 

在伺服器或資料庫連接到 Analysis Services 需要系統管理權限，用於讀取-寫入作業及通過的模擬的連接要求。  

雖然 Analysis Services 安全性基礎結構已經過擴充，以允許在非常特定的情況下的自訂驗證的最近幾年，唯一支援的外部驗證方法是 Windows 整合式的安全性。 安全性主體會假設是有效的 Windows 網域使用者或群組帳戶。  

在 Windows 2012 及更新版本，委派可以被流動的跨網域。 在 Analysis Services 中，委派只適用於 DirectQuery 模型;否則連接會直接或模擬。 

## <a name="next-steps"></a>後續步驟 

建立連接後，邏輯的下一個步驟是已經在伺服器上，其中一個清單中現有的資料庫，或可能是建立新的空白資料庫。 以下連結包括程式碼範例會示範這兩項基本工作： 

- [建立及部署的空白資料庫](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [列出現有的資料庫](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)
