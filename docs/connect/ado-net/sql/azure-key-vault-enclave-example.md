---
title: 示範如何搭配透過安全記憶體保護區啟用的 Always Encrypted 使用 Azure Key Vault 提供者的範例 | Microsoft Docs
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
ms.openlocfilehash: a4ba44733d2a14323f128f1ab105e79169b90cce
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250938"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted-enabled-with-secure-enclaves"></a>示範如何搭配透過安全記憶體保護區啟用的 Always Encrypted 使用 Azure Key Vault 提供者的範例

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

此範例示範如何在存取加密資料行時使用 Azure Key Vault 提供者。

[!code-csharp [Azure Key Vault Provider with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample.cs#1)]

## <a name="see-also"></a>另請參閱

- [示範如何搭配 Always Encrypted 使用 Azure Key Vault 提供者的範例](azure-key-vault-example.md)
- [教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET 應用程式](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [搭配 Microsoft .NET Data Provider for SQL Server 使用 Always Encrypted](sqlclient-support-always-encrypted.md)
