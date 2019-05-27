---
title: 尋找報表定義結構描述版本 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 395392908055a41a8418f02ce3510c050a3447f1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102650"
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>尋找報表定義結構描述版本 (SSRS)
  報表定義檔案會針對用來驗證 rdl 檔的報表定義結構描述版本指定 RDL 命名空間。 當您在報表撰寫環境 (例如 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的報表設計師或報表產生器) 中開啟 .rdl 檔案時，如果此報表是針對先前的命名空間所建立，系統就會自動建立備份檔案，而且此報表會升級為目前的命名空間。 如果您儲存了升級的報表定義，就會儲存轉換的 .rdl 檔。 這是升級報表定義的唯一方式。 報表定義本身不會在報表伺服器上升級。 不過，已編譯的報表會在報表伺服器上升級。 如需詳細資訊，請參閱 [Upgrade Reports](../install-windows/upgrade-reports.md)。  
  
### <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>HOW TO：識別報表的 RDL 結構描述版本  
  
1.  在可以檢視 xml 的應用程式 (例如 [記事本] 或 XML Notepad 2007) 中開啟 .rdl 檔案。  
  
     XML 報表元素會指定結構描述命名空間。 例如，下列報表元素會指定報表設計師的命名空間以及報表定義的命名空間。  
  
    ```  
    <Report xmlns:rd=https://schemas.microsoft.com/SQLServer/reporting/reportdesigner   
    xmlns="https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     報表定義命名空間是由下列 URL 指定： `https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`。  
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>HOW TO：識別報表設計師的 RDL 結構描述版本  
  
1.  開啟新的專案。 您所選擇的專案版本會決定 RDL 結構描述的版本。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中支援多個結構描述版本。 如需詳細資訊，請參閱 [Deployment and Version Support in SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)。  
  
2.  在 [專案] 功能表上，按一下 [加入新項目]。 [新增項目] 對話方塊隨即開啟。  
  
3.  在 [範本] 窗格中，按一下 [報表]。  
  
4.  在 [名稱] 中，鍵入報表名稱或接受預設值。  
  
5.  按一下 **[加入]**。 報表設計師就會在 [設計] 檢視中開啟新的空白報表。  
  
6.  在 [檢視] 功能表中，按一下 [程式碼]。 報表定義就會顯示成 XML 檔。  
  
     XML 報表元素會指定結構描述命名空間。 例如，下列報表元素會指定報表設計師的命名空間以及報表定義的命名空間。  
  
    ```  
    <Report xmlns:rd=https://schemas.microsoft.com/SQLServer/reporting/reportdesigner  
    xmlns="https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     報表定義命名空間是由下列 URL 指定： `https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>HOW TO：識別報表伺服器的 RDL 結構描述版本  
  
-   在報表管理員中，輸入報表伺服器的 URL。 例如，下列 URL 會指定本機電腦上的報表伺服器。  
  
     `http://localhost/reportserver/reportdefinition.xsd`  
  
     .xsd 檔就會在瀏覽器中開啟。  
  
     XML 結構描述元素會指定結構描述命名空間。 例如，下列結構描述元素會指定三個命名空間： [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]在內部使用的 targetNamespace 參考、結構描述本身 (xsd) 的 xsd 參考，以及報表定義參考。  
  
    ```  
    <xsd:schema   
    targetNamespace="https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
    xmlns="https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    elementFormDefault="qualified">  
    ```  
  
     報表定義命名空間是由下列 URL 指定： `https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
## <a name="see-also"></a>另請參閱  
 [Upgrade Reports](../install-windows/upgrade-reports.md)   
 [報表定義語言 &#40;SSRS&#41;](report-definition-language-ssrs.md)  
  
  
