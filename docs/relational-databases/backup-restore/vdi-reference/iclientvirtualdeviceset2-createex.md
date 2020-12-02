---
title: IClientVirtualDeviceSet2::CreateEx
titlesuffix: SQL Server VDI reference
description: 本文提供 IClientVirtualDeviceSet2::CreateEx 命令的參考。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 180ad0ca42904a6a9c4820db1cb5fab36157e972
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125430"
---
# <a name="iclientvirtualdeviceset2createex-vdi"></a>IClientVirtualDeviceSet2::CreateEx (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**CreateEx** 函式會建立虛擬裝置集。

## <a name="syntax"></a>語法

```c
HRESULT IClientVirtualDeviceSet2::CreateEx (
   LPCWSTR         lpInstanceName,
   LPCWSTR         lpName,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>參數

*lpInstanceName* 這個字串會識別 SQL 命令傳送目標的 SQL Server 實例。

*lpName* 這會識別虛擬裝置集。 必須遵循 CreateFileMapping() 所使用的名稱規則。 可使用反斜線 (\) 以外的其他字元。 這是寬字元的 Unicode 字串。 建議在字串前面加上使用者的產品或公司名稱和資料庫名稱。

*pCfg* 這是虛擬裝置集的設定。 如需詳細資訊，請參閱＜設定＞。

## <a name="return-value"></a>傳回值

|傳回值 | 說明 |
|---|---|
| NOERROR | 此函數已成功。 |
| VD_E_NOTSUPPORTED | 設定中的一或多個欄位無效或不受支援。 |
| VD_E_PROTOCOL | 已建立虛擬裝置集。 |

## <a name="remarks"></a>備註

每個 BACKUP 或 RESTORE 作業只能呼叫一次 CreateEx 方法。 叫用 Close 方法之後，用戶端可以重複使用此介面來建立另一個虛擬裝置集。

實例名稱必須識別 Transact-SQL 發出目標的實例。 Null 可識別預設實例。 不接受 "machineName\" 前置詞。

CreateEx (和 Create) 呼叫會在用戶端處理序的處理序控制代碼上修改安全性 DACL。 因此，處理序控制代碼的任何其他修改內容，都必須透過叫用 CreateEx 來進行序列化。 CreateEx 會與 CreateEx 的其他呼叫一起序列化，但是無法使用外部處理進行序列化。 存取權會授與執行 SQL Server 服務的帳戶。

CreateEx 方法會取代原始 IClientVirtualDeviceSet 中所定義的 Create 方法。 原始的 Create 方法已淘汰，不應該用於未來的開發。 原始的 Create 方法會使用 _VIRTUAL_SERVER_NAME_ 環境變數來實作實例名稱支援的形式。 如果在環境中設定該變數，則 Create 方法會在內部呼叫 CreateEx，並傳遞 _VIRTUAL_SERVER_NAME_ 的值作為實例名稱。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [SQL Server 虛擬裝置介面參考概觀](reference-virtual-device-interface.md)。