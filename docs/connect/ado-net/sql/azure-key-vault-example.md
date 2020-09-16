---
description: 示範如何搭配 Always Encrypted 使用 Azure Key Vault 提供者的範例
title: 示範如何搭配 Always Encrypted 使用 Azure Key Vault 提供者的範例 | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: b0f389a822b3fcc37572b34a17cd5780f1091bd4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438660"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted"></a>示範如何搭配 Always Encrypted 使用 Azure Key Vault 提供者的範例

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

此範例示範如何在存取加密資料行時使用 Azure Key Vault 提供者。

[!code-csharp [AKVProvider Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample.cs#1)]

## <a name="see-also"></a>另請參閱

- [示範如何搭配透過安全記憶體保護區啟用的 Always Encrypted 使用 Azure Key Vault 提供者的範例](azure-key-vault-enclave-example.md)
- [教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET 應用程式](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [搭配 Microsoft .NET Data Provider for SQL Server 使用 Always Encrypted](sqlclient-support-always-encrypted.md)
