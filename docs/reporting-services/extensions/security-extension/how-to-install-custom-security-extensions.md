---
title: "如何安裝自訂安全性延伸模組 |Microsoft 文件"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
caps.latest.revision: 3
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 58cfeef7d74e0641b965c307551f0fba4a7ff09c
ms.contentlocale: zh-tw
ms.lasthandoff: 07/11/2017

---

# 如何安裝自訂安全性延伸模組
<a id="how-to-install-custom-security-extensions" class="xliff"></a>

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 2016 導入了新的 web 入口網站以裝載新的 Odata Api，也會裝載新的報表工作負載，例如行動報表和 KPI。 這個新的入口網站必須使用較新的技術，而是與熟悉 ReportingServicesService 隔離個別處理序中執行。 此程序裝載的 ASP.NET 應用程式並不在這種情況會中斷現有的自訂安全性延伸模組的假設。 此外，自訂安全性延伸模組介面目前不允許針對要傳入任何外部內容，讓實作者與唯一的選擇，來檢查已知的通用 ASP.NET 物件，這需要介面的某些變更。

## 變更的項目？
<a id="what-changed" class="xliff"></a>

引進新的介面，可以實作提供 IRSRequestContext 提供延伸模組用於決定與驗證相關的更常見屬性。

在舊版中，報表管理員前端並無法使用它自己的自訂登入頁面設定。 在 Reporting Services 2016 中，只有一個 reportserver 所裝載的分頁支援，且應該驗證這兩個應用程式。

## 實作
<a id="implementation" class="xliff"></a>

在舊版中，擴充功能無法依賴 ASP.NET 物件，就可以輕易地使用常見的假設。 新的入口網站不會在 ASP.NET 中執行，因為擴充功能可能會與 NULL 的物件叫用問題。

大部分的泛型範例來存取 HttpContext.Current 讀取要求的資訊，例如標頭和 cookie。 為了讓擴充功能相同做出我們引進了新的方法中的延伸模組，提供要求資訊並驗證從入口網站時，會呼叫。 

延伸模組必須實作<xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2>為了充分利用這個介面。 延伸模組必須實作兩個版本的<xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A>方法，如稱為 reportserver 內容和其他 webhost 程序中使用。 下列範例顯示其中一種簡單的實作，其中由 reportserver 解決的身分識別是用入口網站。

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

## 部署和設定
<a id="deployment-and-configuration" class="xliff"></a>

自訂安全性延伸模組所需的基本組態會與舊版相同。 變更所需的 web.config 和 rsreportserver.config： 如需詳細資訊，請參閱[設定自訂或表單驗證，在報表伺服器上](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)。

不會再個別報表管理員的 web.config，入口網站將會繼承 reportserver 端點的相同設定。

## 電腦金鑰
<a id="machine-keys" class="xliff"></a>

需要驗證 cookie 的解密表單驗證的案例中，必須使用相同的電腦金鑰和解密演算法來設定這兩個處理程序。 這種不熟悉的使用者先前已安裝 Reporting Services 向外延展環境上運作，但現在是甚至在單一機器上部署的需求的步驟。

您應該使用驗證您部署的特定索引鍵，有數個工具來產生金鑰像網際網路資訊服務管理員 (IIS)。 其他工具可以在網際網路上找到。

### SQL Server Reporting Services 2017 和更新版本
<a id="sql-server-reporting-services-2017-and-later" class="xliff"></a>

**\ReportServer\rsReportServer.config**

將新增之下`<configuration>`。

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### SQL Server Reporting Services 2016
<a id="sql-server-reporting-services-2016" class="xliff"></a>

**\ReportServer\web.config**

將新增之下`<system.web>`。
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

將新增之下`<configuration>`。

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### Power BI 報表伺服器
<a id="power-bi-report-server" class="xliff"></a>

這是從年 6 月 2017 （建置 14.0.600.301） 版開始，您可以使用。

**\ReportServer\rsReportServer.config**

將新增之下`<configuration>`。

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## 設定通過 cookie
<a id="configure-passthrough-cookies" class="xliff"></a>

新的入口網站和 reportserver 內部 soap Api 使用某些作業 （類似於舊版的報表管理員） 進行通訊。 從入口網站會傳遞至伺服器所需的其他 cookie PassThroughCookies 屬性時，仍然可以使用。 如需詳細資訊，請參閱[設定入口網站，以傳遞自訂驗證 Cookie](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)。

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## 後續的步驟
<a id="next-steps" class="xliff"></a>

[設定報表伺服器上的自訂或表單驗證](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[設定報表管理員傳遞自訂驗證 Cookie](https://msdn.microsoft.com/library/ms345241(v=sql.120).aspx)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
