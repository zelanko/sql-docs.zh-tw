---
title: 啟用外部指令碼伺服器設定選項 | Microsoft Docs
ms.date: 11/13/2017
ms.prod: sql
ms.technology: configuration
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords:
- external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3f47352cc82ac831ebcd64548baa24423490094f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "72006044"
---
# <a name="external-scripts-enabled-server-configuration-option"></a>啟用外部指令碼伺服器設定選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

使用 **external scripts enabled** 選項以啟用具有特定遠端語言擴充功能之指令碼的執行。 依預設，此屬性為 OFF。 如果已安裝**進階分析服務**，安裝程式就可以選擇將此屬性設定為 true。

## <a name="remarks"></a>備註

您必須先啟用 external script enabled 選項，才能使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 程序來執行外部指令碼。 使用 **sp_execute_external_script** 執行以所支援語言 (例如 R 或 Python) 所撰寫的指令碼。 

+ 針對 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]

    [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支援 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中的 R 語言，以及一組 R 工作站工具和連線程式庫。

    在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式期間安裝 [進階分析擴充功能]  功能，以啟用 R 指令碼的執行。 預設會安裝 R 語言。

+ 針對 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]

    [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 使用與 SQL Server 2016 相同的結構，但支援 Python 語言。

    在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式期間安裝 [進階分析擴充功能]  功能，以啟用外部指令碼的執行。 請務必在初始安裝期間選取至少一個語言：R、Python 或兩者。 

## <a name="additional-requirements"></a>其他需求

安裝後，若要啟用外部指令碼，請執行下列指令碼：

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

您必須重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，讓這項變更生效。

如需詳細資訊，請參閱[設定 SQL Server Machine Learning](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。

## <a name="see-also"></a>另請參閱

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)

[sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

[SQL Server Machine Learning 服務](../../advanced-analytics/r/sql-server-r-services.md)
