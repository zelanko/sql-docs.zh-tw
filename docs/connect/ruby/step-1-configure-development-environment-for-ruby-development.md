---
title: 步驟 1︰設定 PHP 開發的開發環境 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1de9ce8b14dd164ac24ac1bb7098494dbc134bfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778256"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>步驟 1︰設定 Ruby 開發的開發環境
您必須設定您的開發環境的先決條件，才能開發使用 Ruby Driver for SQL Server 的應用程式。    
  
請注意，Ruby 驅動程式會使用 TDS 通訊協定，SQL Server 和 Azure SQL Database 中的預設會啟用。  不需要進行其他組態設定。  
  
  
## <a name="windows"></a>Windows  
  
1.  **Ruby 的安裝程式下載**  
如果您的電腦並沒有 Ruby 請加以安裝。 針對新的 ruby 使用者，我們建議使用 Ruby 2.2.x 版本安裝程式。 這些提供穩定的語言和廣泛相容，並且已更新的封裝 （寶藏） 清單。 移[Ruby 的下載頁面](http://rubyinstaller.org/downloads/)及下載適當的 2.1.x 安裝程式。 如範例中，如果您是在 64 位元電腦上，下載 Ruby 2.1.6 (x64) 安裝程式。   
  
2.  **安裝 Ruby**  
安裝程式下載後，執行下列作業：  
A. 按兩下檔案以啟動安裝程式。  
B. 選取您的語言，並同意條款。  
c.  在 [安裝設定] 畫面中，選取您路徑並產生關聯.rb 和.rbw 檔案這項 Ruby 安裝這兩個新增的 Ruby 可執行檔旁邊的核取方塊。  
  
3.  **下載 Ruby DevKit**  
從 RubyInstaller 頁面下載 DevKit  
  
4.  **安裝 Ruby DevKit**  
下載完成之後，執行下列作業：  
A. 按兩下檔案。 您必須將檔案解壓縮的位置。  
B. 按一下 [...] 按鈕，然後選取 「 C:\DevKit"。 您可能必須先建立此資料夾，依序按一下 [讓新資料夾]。  
c. 按一下 [確定]，並接著 [擷取]，將檔案解壓縮。  
  
5. **開啟 cmd.exe**  
  
6. **初始化 Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **安裝 TinyTDS gem**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux 17.10  
  
1. **開啟終端機**  
  
2. **安裝 Ruby 版本管理員 (rvm) 和必要條件**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **安裝 Ruby 使用 rvm**  
例如，安裝 Ruby 的版本 2.3.0:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;請確定最後一個命令的輸出，表示您正在 2.3.0 版。  
  
4.  **安裝 FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **安裝 TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
請注意，Mac OS X 已經 Ruby 預先安裝，因為作業系統具有相依性。    
  
1.  **開啟終端機**  
  
2. **安裝 Homebrew 套件管理員**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **安裝 FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **安裝 TinyTDS gem**  
```  
> gem install tiny_tds  
```
