---
title: 使用我的報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 49c3c1da-b106-41f6-9173-16ff225bade8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 29e7003beeb5daa331a16c572994b4bb1a6ec6d4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59955804"
---
# <a name="using-my-reports-report-builder-and-ssrs"></a>使用我的報表 (報表產生器及 SSRS)
  在設定為原生模式的報表伺服器上，[我的報表] 資料夾是個人的工作空間，可以用來儲存和使用您所擁有的報表。 其他報表伺服器資料夾都是公開的，通常使用者必須具備進階權限才可以加入或修改資料夾內容。 相對地，[我的報表] 資料夾是使用者自行管理的工作空間。 您可以加入或移除報表和資料夾，以及使用個人化的設定來儲存連結報表。  
  
 在概念上，[我的報表] 資料夾類似於 Windows 檔案系統的 [我的文件] 資料夾。 雖然每一位使用者都有稱為 [我的報表] 的資料夾，但每一位使用者存取的資料夾與其他人都不相同。 除了報表伺服器管理員之外，其他使用者都無法存取屬於您的 [我的報表] 資料夾的內容。  
  
 [我的報表] 功能是選擇性的，可以由報表伺服器管理員停用。 如果有啟用「我的報表」，您就會在 [主資料夾] 資料夾中看到 [我的報表] 資料夾，您可以使用報表管理員或 Web 瀏覽器來存取其內容。 如需詳細資訊，請參閱[在報表管理員中尋找及檢視報表 &#40;報表產生器及 SSRS&#41;](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)。  
  
 在設定為 SharePoint 整合模式的報表伺服器上，[我的報表] 資料夾沒有任何對等項目。 如需詳細資訊，請參閱 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="ways-to-use-my-reports"></a>使用我的報表的方式  
 在您加入報表、資料夾和其他項目之前，[我的報表] 是空的。 以下是將內容加入至 [我的報表] 的一些方法。  
  
-   建立個人的連結報表，並將它儲存至 [我的報表]。 並非所有的報表都可以連結。 如需詳細資訊，請參閱 [建立連結報表](../reports/create-a-linked-report.md)。  
  
-   從檔案系統上傳報表定義檔 (.rdl)、報表模型檔 (.smdl) 或其他檔案。 您可以上傳任何檔案，但報表伺服器只會處理副檔名為 .rdl 或 .smdl 的報表檔案。 如需詳細資訊，請參閱《SQL Server 線上叢書》中 [Reporting Services 文件](https://go.microsoft.com/fwlink/?linkid=121312)的＜報表定義＞以及[上傳檔案或報表 &#40;報表管理員&#41;](../reports/upload-a-file-or-report-report-manager.md)。  
  
-   建立並發行自己的報表至 [我的報表]。 如需詳細資訊，請參閱[報表設計檢視 &#40;報表產生器&#41;](report-design-view-report-builder.md)。  
  
 通常 [我的報表] 的權限設定，可以讓您自行管理此資料夾。 不過，報表伺服器管理員才是最終決定使用者可執行哪些工作的人。 如果因權限不足而無法使用 [我的報表]，請洽詢報表伺服器管理員。  
  
## <a name="searching-my-reports"></a>搜尋 [我的報表]  
 在搜尋報表伺服器資料庫時，[我的報表] 資料夾的內容將包含在搜尋中，但是會排除其他使用者的 [我的報表] 資料夾的內容。 搜尋結果清單只會包含您有權存取的報表。  
  
## <a name="see-also"></a>另請參閱  
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
