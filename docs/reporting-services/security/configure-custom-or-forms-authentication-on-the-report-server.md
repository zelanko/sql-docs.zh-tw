---
title: 設定報表伺服器上的自訂或表單驗證 | Microsoft Docs
ms.date: 04/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8c77e0f066c6342fb0b5bc58130cb20c80e40de3
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571162"
---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>設定報表伺服器上的自訂或表單驗證

Reporting Services 提供可延伸的架構，可以讓您插入自訂或表單型驗證延伸模組。 如果部署需求不包含 Windows 整合式安全性或基本驗證，您可能會考慮實作自訂驗證延伸模組。 使用自訂驗證最常見的狀況是支援網際網路或外部網路對 Web 應用程式的存取。 以自訂的驗證延伸模組取代預設的 Windows 驗證延伸模組時，可讓您進一步控制如何授與外部使用者存取報表伺服器的權限。  

實際上，部署自訂驗證延伸模組所需的多個步驟包括複製組件和應用程式檔案、修改組態檔，以及測試。 本主題只著重於您在組態檔中所指定的驗證設定。  

> [!NOTE]
>  建立自訂驗證延伸模組時，需要自訂的程式碼和 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 安全性的專業知識。 如果您不想要建立自訂驗證延伸模組，可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 群組與帳戶，但必須大幅縮減報表伺服器部署的範圍。 如需自訂驗證的詳細資訊，請參閱 [實作安全性延伸模組](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)。

此外，如果想要在與 SharePoint 產品整合的 SQL Server Reporting Services 環境中，使用表單驗證或自訂驗證延伸模組，必須將 SharePoint 網站設定為使用您選擇的驗證方法。 如需在 SharePoint 中設定驗證的詳細資訊，請參閱 [Developer Network (MSDN) 上的](https://go.microsoft.com/fwlink/?LinkId=115575) 驗證範例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。



### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>設定報表伺服器以使用自訂驗證

1.  在文字編輯器中開啟 RSReportServer.config。

2.  尋找 \<**驗證**>。

3.  複製下列 XML 結構：

    ```
    <Authentication>
          <AuthenticationTypes>
                 <Custom />
          </AuthenticationTypes>
          <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    ```

4.  將它貼到 \<**驗證**> 的現有項目上。

     請注意，您無法搭配其他驗證類型使用 **Custom** 。

5.  儲存檔案。

6.  開啟報表伺服器的 Web.config 檔。 根據預設，它位於 \Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer。

7.  尋找 **authentication mode** ，並將它設為 **Forms**。

    ```
    <authentication mode = "Forms" />
    ```

8.  尋找 **identity impersonate** ，並將它設為 **False**。

    ```
    <identity impersonate = "false" />  
    ```
9. 將 **PassThroughCookies** 元素結構加入至組態檔中。 如需詳細資訊，請參閱[設定入口網站傳遞自訂驗證 Cookie](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
10. 儲存檔案。  
  
11. 如果您設定了向外延展部署，請針對部署中的其他報表伺服器重複先前所有的步驟。  
  
12. 重新啟動報表伺服器，清除目前開啟的任何工作階段。  

## <a name="see-also"></a>另請參閱

[實作安全性延伸模組](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
[Reporting Services 自訂安全性範例 (GitHub)](https://github.com/Microsoft/Reporting-Services/tree/master/CustomSecuritySample)  
[使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)   
[RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[設定報表伺服器上的基本驗證](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
[設定報表伺服器上的 Windows 驗證](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
