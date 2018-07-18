---
title: 連接到現有的 Analysis Services 表格式伺服器和資料庫 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13900e4aaad52d39a2691fb40d0e419f55f660fc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033388"
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>連接到現有的 Analysis Services 表格式伺服器和資料庫
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
在 SQL Server 2016 Analysis Services 管理物件 (AMO) 會包含數個可用來設定伺服器連接的命名空間。 這篇文章說明如何建立伺服器連線的 Microsoft.AnalysisServices.Tabular 命名空間用於模型和資料庫建立在 1200年或更高的相容性層級。 

若要連接到 Analysis Services 伺服器，您的程式碼必須具現化伺服器物件，並接著在其上呼叫 Connect 方法。 連線之後，伺服器物件的屬性會反映目前的 Analysis Services 執行個體的設定。 

下列類別可用於最上層的連線： 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

如您所見，兩個命名空間提供的伺服器和資料庫物件的連接： AMO 的原始 Microsoft.AnalysisServices 命名空間和新的 Microsoft.AnalysisServices.Tabular 命名空間，如 TOM。

為什麼要進行相同的作業的兩個命名空間？ 答案就是下游，其中物件階層會變成模式特定，而模型樹狀結構由多維度或表格式中繼資料所組成的資料庫和模型層級。 若要呼叫模型樹狀結構中，這兩種模型類型提供的伺服器或資料庫物件。

> [!NOTE]  
>  使用模型定義和作業的中繼資料是完全不同的兩種模式。 藉由分隔到兩個不同的命名空間的資料定義語言 (DDL)，開發經驗已經過簡化透過只需要針對特定模型類型的 API 的呈現方式。 

雖然 DDL 不同，伺服器的連線都相同模式、 版本和版本。 支援的伺服器和資料庫連接，透過任一個命名空間可讓您撰寫泛型的工具或連接到任何 Analysis Services 執行個體的指令碼，或資料庫，而不需要知道何種模型裝載在伺服器上。  

這種彈性說明的組件之間的相依性。 若要呼叫下列資料庫層級 （例如，在表格式 1200年資料庫內的模型或 Cube、 維度或 MeasureGroup 多維度或表格式 1050年-1103年資料庫內），AMO 會對 TOM 相依性。 

相反地，TOM 沒有相依性上 AMO。 雖然 TOM 無法用來瀏覽多維度中繼資料 (Cube) 中，AMO 可用來瀏覽多維度與表格式中繼資料。 

基於這個理由，您的專案所設定的第一個步驟會需要將參考加入至所有的 AMO 組件。 請參閱[安裝，請參考及散發 TOM 用戶端程式庫](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)如需詳細資訊。 

> [!NOTE]  
>  伺服器和資料庫的連線根據舊版 AMO 類別繼承自 MajorObject。 主要和次要物件不使用表格式模型樹狀結構中，但是 MajorObject 類別是伺服器和資料庫物件，不論哪一個 API，您使用設定連線的基底類別為可見的。  

## <a name="code-example-server-connection"></a>程式碼範例： 伺服器連接 

以下是 C# 程式碼範例，示範如何連接到本機的 Analysis Services 執行個體，並列出其在主控台視窗中的屬性。 

此範例只會顯示部分內容的伺服器物件，但有更多屬性，包括 ServerMode 和 DefaultCompatibilityLevel。  

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

伺服器或資料庫連接到 Analysis Services 需要系統管理權限，用於讀寫作業及通過的模擬的連接要求。  

雖然 Analysis Services 安全性基礎結構已經過擴充，近幾年來，以允許自訂的驗證，在非常特定的情況下，唯一支援的外部驗證方法是 Windows 整合式的安全性。 安全性主體會假設為有效 Windows 網域使用者或群組帳戶。  

在 Windows 2012 和更新版本中，委派可以被流動的跨網域。 在 Analysis Services 中，僅適用於 DirectQuery 模式中，使用委派否則，連線會直接或模擬。 

## <a name="next-steps"></a>後續的步驟 

建立連接後，邏輯的下一個步驟是已經在伺服器上，任一個列出的現有資料庫，或可能是建立新的空白資料庫。 以下連結包括程式碼範例會示範這兩項基本工作： 

- [建立及部署空白資料庫](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [列出現有的資料庫](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)
