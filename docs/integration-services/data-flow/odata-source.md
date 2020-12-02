---
description: OData 來源
title: OData 來源 | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
- sql13.dts.designer.odatasource.connection.f1
- sql13.dts.designer.odatasource.columns.f1
- sql13.dts.designer.odatasource.erroroutput.f1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8f872916b7b93a1aab3447bad6579dd672c915e1
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194793"
---
# <a name="odata-source"></a>OData 來源

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


使用 SSIS 封裝中的 OData 來源元件，從開放式資料通訊協定 (OData) 服務取用資料。

## <a name="supported-protocols-and-data-formats"></a>支援的通訊協定和資料格式

此元件支援 OData v3 和 v4 通訊協定。  
  
-   針對 OData V3 通訊協定，此元件支援 ATOM 和 JSON 資料格式。  
  
-   針對 OData V4 通訊協定，此元件支援 JSON 資料格式。  

## <a name="supported-data-sources"></a>支援的資料來源

OData 來源包含下列資料來源的支援：
-   Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online
-   SharePoint 清單。 若要查看 SharePoint 伺服器上的所有清單，請使用下列 URL：`https://<server>/_vti_bin/ListData.svc`。 如需 SharePoint URL 慣例的詳細資訊，請參閱 [SharePoint Foundation REST 介面](/previous-versions/office/developer/sharepoint-2010/ff521587(v=office.14))。

## <a name="supported-data-types"></a>支援的資料類型

OData 來源支援下列簡單資料類型：int、byte[]、bool、byte、DateTime、DateTimeOffset、decimal、double、Guid、Int16、Int32、Int64、sbyte、float、string 和 TimeSpan。

若要探索您資料來源中資料行的資料類型，請檢查 `https://<OData feed endpoint>/$metadata` 頁面。

針對 **Decimal** 資料類型，有效位數和小數位數是由來源中繼資料所決定。 如果來源中繼資料未指定 **Precision** 和 **Scale** 屬性，則資料可能會被截斷。

> [!IMPORTANT]
> OData 來源元件不支援 SharePoint 清單中的複雜類型，例如多重選擇項目。

> [!Note]
> 若來源僅允許 TLS 1.2 連線，則需要在電腦上透過登錄設定來實施 TLS 1.2。 在提高權限的命令提示字元中執行下列命令：
>
> reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SchUseStrongCrypto /t REG_DWORD /d 1 /reg:64
>
> reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SchUseStrongCrypto /t REG_DWORD /d 1 /reg:32

## <a name="odata-format-and-performance"></a>OData 格式和效能
 大部分的 OData 服務都會傳回多種格式的結果。 您可使用 `$format` 查詢選項來指定結果集的格式。 類似 JSON 和 JSON Light 的格式要比 ATOM 或 XML 更有效率，而且在傳輸大量資料時可能會提供更好的效能。 下表提供範例測試的結果。 如您所見，當從 ATOM 切換到 JSON 時有 30-53% 的效能提升，而且當從 ATOM 切換到新的 JSON light 格式時有 67% 的效能提升 (適用於 WCF Data Services 5.1)。  
  
|資料列|ATOM|JSON|JSON (Light)|  
|-|-|-|-|  
|10000|113 秒|74 秒|68 秒|  
|1000000|1110 秒|853 秒|665 秒|  
  
## <a name="related-topics-in-this-section"></a>本節中的相關主題  
  
-   [教學課程：使用 OData 來源](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [在執行階段修改 OData 來源查詢](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [OData 來源屬性](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="odata-source-editor-connection-page"></a>OData 來源編輯器 (連接頁面)
  使用 **[OData 來源編輯器]** 對話方塊的 **[連接]** 頁面，選取 OData 來源的 OData 連接管理員。 此頁面也可讓您指定集合或資源路徑及任何查詢選項，以指示需要從 OData 來源擷取哪些資料。 
  
### <a name="static-options"></a>靜態選項  
 **OData 連接管理員**  
 從清單中選取現有的連線管理員，或按一下 [新增]  來建立新的連線。  
  
 在您選取或建立連接管理員之後，對話方塊會顯示連接管理員正在使用的 OData 通訊協定版本。  
  
 **新增**  
 使用 [OData 連線管理員編輯器] 對話方塊建立新的連線管理員。  
  
 **使用集合或資源路徑**  
 從來源中指定選取資料的方法。  
  
|選項|描述|  
|------------|-----------------|  
|集合|使用集合名稱從 OData 來源擷取資料。|  
|資源路徑|使用資源路徑從 OData 來源擷取資料。|  
  
 **查詢選項**  
 指定查詢的選項。 例如：`$top=5` 
  
 **摘要 url**  
 根據您在此對話方塊中選取的選項顯示唯讀摘要 URL。  
  
 **預覽**  
 使用 [預覽] 對話方塊來預覽結果。 **[預覽]** 最多可顯示 20 個資料列。  
  
### <a name="dynamic-options"></a>動態選項  
  
#### <a name="use-collection-or-resource-path--collection"></a>使用集合或資源路徑 = 集合  
 **集合**  
 從下拉式清單中選取集合。  
  
#### <a name="use-collection-or-resource-path--resource-path"></a>使用集合或資源路徑 = 資源路徑  
 **Resource path**  
 輸入資源路徑。 例如：員工  
  
## <a name="odata-source-editor-columns-page"></a>OData 來源編輯器 (資料行頁面)
  使用 [OData 來源編輯器] 對話方塊的 [資料行] 頁面，選取要包含在輸出中的外部 (來源) 資料行，並將其對應到輸出資料行。  
  
### <a name="options"></a>選項。  
 **可用的外部資料行**  
 在資料來源中檢視可用的來源資料行清單。 使用清單中的核取方塊，為頁面底部的資料表加入或移除資料行。 選取的資料行會新增至輸出。  
  
 **[外部資料行]**  
 檢視您選擇要包含在輸出中的來源資料行。  
  
 **輸出資料行**  
 為每個輸出資料行提供唯一的名稱。 預設值為選取的外部 (來源) 資料行的名稱；不過，您也可以選擇任何唯一的、描述性的名稱。  
  
## <a name="odata-source-editor-error-output-page"></a>OData 來源編輯器 (錯誤輸出頁面)
  使用 [OData 來源編輯器] 對話方塊的 [錯誤輸出] 頁面，選取錯誤處理選項，並設定錯誤輸出資料行上的屬性。  
  
### <a name="options"></a>選項。  
 **輸入/輸出**  
 檢視資料來源的名稱。  
  
 **資料行**  
 檢視您在 [OData 來源編輯器] 對話方塊的 [連線管理員] 頁面上所選取的外部 (來源) 資料行。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題：** [資料中的錯誤處理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 指定截斷發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **說明**  
 檢視錯誤的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [OData 連接管理員](../../integration-services/connection-manager/odata-connection-manager.md)  
  
