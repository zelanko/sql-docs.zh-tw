---
title: 第 1 課： 建立 RDL 結構描述 Visual Studio 專案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f420509c-51aa-4170-8c25-64c2954f4bb9
caps.latest.revision: 17
author: craigg-msft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc69b4bbcc40fa669ca9cf5f889944cb302e4b14
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319808"
---
# <a name="lesson-1-create-the-rdl-schema-visual-studio-project"></a>第 1 課：建立 RDL 結構描述 Visual Studio 專案
  在這個教學課程中，您會建立簡單的主控台應用程式。 本教學課程假設您正在開發中[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]。  
  
> [!NOTE]  
>  當您存取在 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services 上執行的報表伺服器 Web 服務時，必須將 "_SQLExpress" 附加至 "ReportServer" 路徑。 例如：  
>   
>  `http://myserver/reportserver_sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-create-the-web-service-proxy"></a>若要建立 Web 服務 Proxy  
  
1.  從**開始**功能表上，選取**所有程式**、 Microsoft Visual Studio，然後**Visual Studio Tools**，然後**Visual Studio 2010 命令提示字元**.  
  
2.  如果您是使用 C#，請在命令提示字元視窗中執行下列命令：  
  
    ```  
    wsdl /language:CS /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     如果您是使用 Visual Basic，則請在執行下列命令：  
  
    ```  
    wsdl /language:VB /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     這個命令會產生 .cs 或 .vb 檔案。 您會將這個檔案加入應用程式中。  
  
### <a name="to-create-a-console-application"></a>若要建立主控台應用程式  
  
1.  上**檔案**功能表上，指向**新增**，然後按一下**專案**以開啟**新專案** 對話方塊。  
  
2.  在左窗格中，在**已安裝的範本**，按一下**Visual Basic**或**Visual C#** 節點，然後選取專案的類別類型從展開的清單。  
  
3.  選擇**主控台應用程式**專案類型。  
  
4.  在 **名稱**方塊中，輸入您專案的名稱。 輸入名稱`SampleRDLSchema`。  
  
5.  在 **位置**方塊中，輸入您想要用來儲存您的專案，或按一下 的路徑**瀏覽**瀏覽至資料夾。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 您的專案的摺疊的檢視會顯示在 [方案總管] 中。  
  
7.  在 [專案] 功能表上，按一下 [新增現有項目]。  
  
8.  巡覽至的位置，為.cs 或.vb 檔案來產生，然後選取檔案，然後按一下 **新增**。  
  
     您也必須加入 <xref:System.Web.Services> 命名空間的參考，才能讓 Web 參考運作。  
  
9. 在 專案 功能表中，按一下 **加入參考**。  
  
     在**加入參考**對話方塊中，於 **.NET**索引標籤上，選取**System.Web.Services**，然後按一下**確定**。  
  
     如需如何連接到報表伺服器 Web 服務的詳細資訊，請參閱[使用 Web 服務和.NET Framework 建置應用程式](../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
10. 在 [方案總管] 中，展開專案節點。 您會看到含有預設名稱 Program.cs (在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中則為 Module1.vb) 的程式碼檔案已加入專案中。  
  
11. 開啟 Program.cs (在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中為 Module1.vb) 檔案，然後將程式碼取代成下列項目：  
  
     下列程式碼提供方法 stubs，我們將用來實作「載入」、「更新」和「儲存功能」。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using System.Xml.Serialization;  
    using ReportService2010;  
  
    namespace SampleRDLSchema  
    {  
        class ReportUpdater  
        {  
            ReportingService2010 _reportService;  
  
            static void Main(string[] args)  
            {  
                ReportUpdater reportUpdater = new ReportUpdater();  
                reportUpdater.UpdateReport();  
            }  
  
            private void UpdateReport()  
            {  
                try  
                {  
                    // Set up the Report Service connection  
                    _reportService = new ReportingService2010();  
                    _reportService.Credentials =  
                        System.Net.CredentialCache.DefaultCredentials;  
                    _reportService.Url =  
                       "http://<Server Name>/reportserver/" +  
                                       "reportservice2010.asmx";  
  
                    // Call the methods to update a report definition  
                    LoadReportDefinition();  
                    UpdateReportDefinition();  
                    PublishReportDefinition();  
                }  
                catch (Exception ex)  
                {  
                    System.Console.WriteLine(ex.Message);  
                }  
            }  
  
            private void LoadReportDefinition()  
            {  
                //Lesson 3: Load a report definition from the report   
                //          catalog  
            }  
  
            private void UpdateReportDefinition()  
            {  
                //Lesson 4: Update the report definition using the    
                //          classes generated from the RDL Schema  
            }  
  
            private void PublishReportDefinition()  
            {  
                //Lesson 5: Publish the updated report definition back   
                //          to the report catalog  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Imports System  
    Imports System.Collections.Generic  
    Imports System.IO  
    Imports System.Text  
    Imports System.Xml  
    Imports System.Xml.Serialization  
    Imports ReportService2010  
  
    Namespace SampleRDLSchema  
  
        Module ReportUpdater  
  
            Private m_reportService As ReportingService2010  
  
            Public Sub Main(ByVal args As String())  
  
                Try  
                    'Set up the Report Service connection  
                    m_reportService = New ReportingService2010  
                    m_reportService.Credentials = _  
                        System.Net.CredentialCache.DefaultCredentials  
                    m_reportService.Url = _  
                        "http:// <Server Name>/reportserver/" & _  
                               "reportservice2010.asmx"  
  
                    'Call the methods to update a report definition  
                    LoadReportDefinition()  
                    UpdateReportDefinition()  
                    PublishReportDefinition()  
                Catch ex As Exception  
                    System.Console.WriteLine(ex.Message)  
                End Try  
  
            End Sub  
  
            Private Sub LoadReportDefinition()  
                'Lesson 3: Load a report definition from the report   
                '          catalog  
            End Sub  
  
            Private Sub UpdateReportDefinition()  
                'Lesson 4: Update the report definition using the   
                '          classes generated from the RDL Schema  
            End Sub  
  
            Private Sub PublishReportDefinition()  
                'Lesson 5: Publish the updated report definition back   
                '          to the report catalog  
            End Sub  
  
        End Module  
  
    End Namespace   
    ```  
  
## <a name="next-lesson"></a>下一課  
 在下一課，您將使用 XML 結構描述定義工具 (Xsd.exe)，從 RDL 結構描述產生類別，並將類別包含在專案之中。 請參閱[第 2 課： 使用 xsd 工具的 RDL 結構描述的產生類別](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用從 RDL 結構描述產生的類別更新報表&#40;SSRS 教學課程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [報表定義語言 &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
