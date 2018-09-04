---
title: 如何安裝自訂安全性延伸模組 | Microsoft Docs
ms.date: 07/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.suite: pro-bi
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 103d852f27f2f70f598a4bf1d09bb59fcdbcb8d8
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274896"
---
# <a name="how-to-install-custom-security-extensions"></a>如何安裝自訂安全性延伸模組

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016 推出新的入口網站，以裝載新的 Odata API，同時也裝載新的報表工作負載，例如行動報表和 KPI。 這個新的入口網站使用較新的技術，透過在個別的處理序中執行與熟悉的 ReportingServicesService 隔離。 此程序不是 ASP.NET 裝載的應用程式，因此會中斷現有的自訂安全性延伸模組的假設。 此外，自訂安全性延伸模組的現有介面不允許傳入任何外部內容，讓實作者只能選擇檢查已知的通用 ASP.NET 物件，這需要對介面進行部分變更。

## <a name="what-changed"></a>變更了什麼？

可以實作引進的新介面，這會提供 IRSRequestContext，它可提供延伸模組使用的更常見屬性，執行與驗證相關的決定。

在舊版中，報表管理員是前端，可使用自己的自訂登入頁面設定。 在 Reporting Services 2016 中，只支援一個 reportserver 裝載的頁面，但兩個應用程式都應該驗證。

## <a name="implementation"></a>實作

在舊版中，延伸模組只能依賴 ASP.NET 物件應該就緒的常見假設。 因為新的入口網站不會在 ASP.NET 中執行，所以延伸模組可能會引發 NULL 物件問題。

大部分的泛型範例是存取 HttpContext.Current 以讀取要求的資訊，例如標頭和 Cookie。 為了讓延伸模組做出相同的決定，我們在提供要求資訊的延伸模組中引進了新的方法，並在入口網站要求驗證時予以呼叫。 

延伸模組必須實作 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> 介面以充分利用它。 延伸模組需要實作兩個版本的 <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> 方法，一個供 reportserver 內容呼叫，另一個用於 webhost 程序中。 下例示範其中一種簡單的入口網站實作，使用由 reportserver 解析的身分識別。

``` 
public void GetUserInfo(IRSRequestContext requestContext, out IIdentity userIdentity, out IntPtr userId)
{
    userIdentity = null;
    if (requestContext.User != null)
    {
        userIdentity = requestContext.User;
    }

    // initialize a pointer to the current user id to zero
    userId = IntPtr.Zero;
}
```

## <a name="deployment-and-configuration"></a>部署與設定

自訂安全性延伸模組所需的基本設定與舊版相同。 web.config 和 rsreportserver.config 需要變更：如需詳細資訊，請參閱[設定報表伺服器上的自訂或表單驗證](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)。

報表管理員不會再有個別的 web.config，入口網站會繼承與 reportserver 端點相同的設定。

## <a name="machine-keys"></a>電腦金鑰

在需要解密驗證 Cookie 的表單驗證案例中，兩個處理程序都需要使用相同的電腦金鑰和解密演算法設定。 這對已在向外延展環境上設定 Reporting Services 運作的使用者很熟悉，但現在即使是單一電腦部署也是必要步驟。

您應該為部署使用特定的驗證金鑰，有數種工具可以產生金鑰，例如網際網路資訊服務管理員 (IIS)。 網際網路上可以找到其他工具。

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 和更新版本

**\ReportServer\rsReportServer.config**

新增於 `<configuration>` 之下。

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

新增於 `<system.web>` 之下。
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

新增於 `<configuration>` 之下。

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Power BI 報表伺服器

自 2017 年 6 月 2017 (組建 14.0.600.301) 版本開始提供。

**\ReportServer\rsReportServer.config**

新增於 `<configuration>` 之下。

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>設定通過 Cookie

新入口網站和 reportserver 的通訊使用某些作業的內部 SOAP  API (類似於舊版的報表管理員)。 當其他 Cookie 需要從入口網站傳遞至伺服器時，仍然可以使用 PassThroughCookies 屬性。 如需詳細資訊，請參閱 [設定入口網站傳遞自訂驗證 Cookie](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)。

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="next-steps"></a>後續步驟

[設定報表伺服器上的自訂或表單驗證](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[設定報表管理員傳遞自訂驗證 Cookie](../../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
