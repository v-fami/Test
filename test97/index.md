---
title: 変更をアーティクルに反映する方法の設定 (トランザクション )
description: SQL Server Management Studio (SSMS) または Transact-SQL (T-SQL) を使用して、トランザクション レプリケーションのトランザクション アーティクルへのデータの変更の反映方法を設定する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
- propagating data changes [SQL Server replication]
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 00ab2a45675b237e3e15e340cc3789b1b79cdafc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287553"
---
# <a name="set-the-propagation-method-for-data-changes-to-transactional-articles"></a>データの変更をトランザクション アーティクルに反映する方法の設定

  
 既定では、トランザクション レプリケーションは、各アーティクルのストアド プロシージャ セットを使用して変更内容をサブスクライバーに反映します。 これらのプロシージャはカスタム プロシージャに置換することができます。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   **データの変更をトランザクション アーティクルに反映する方法を設定するために、使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## <a name="before-you-begin"></a>はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   レプリケーションによって生成されたスナップショット ファイルを編集する場合には注意が必要です。 カスタム ストアド プロシージャのカスタム ロジックをテストしてサポートする必要があります。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 反映方法は、パブリケーションの新規作成ウィザードからアクセスできる **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスおよび **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[プロパティ]** タブで指定します。 ウィザードの使用およびダイアログ ボックスへのアクセスの詳細については、「[パブリケーションの作成](../../../relational-databases/replication/publish/create-a-publication.md)」および「[View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」 (パブリケーション プロパティの表示および変更) を参照してください。  
  
#### <a name="to-specify-the-propagation-method"></a>反映方法を指定するには  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスでテーブルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  **[反転表示されたテーブル アーティクルのプロパティを設定]** をクリックします。  
  
3.  **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[ステートメントの配信]** セクションで、**[INSERT 配信形式]**、**[UPDATE 配信形式]**、**[DELETE 配信形式]** の各メニューを使用して各操作の反映方法を指定します。  
   
  
5.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  

#### <a name="to-generate-and-use-custom-stored-procedures"></a>カスタム ストアド プロシージャを生成して使用するには  
  
1.  パブリケーションの新規作成ウィザードの **[アーティクル]** ページ、または **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスでテーブルを選択し、 **[アーティクルのプロパティ]** をクリックします。  
  
2.  **[反転表示されたテーブル アーティクルのプロパティを設定]** をクリックします。  
  
     **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスの **[プロパティ]** タブの **[ステートメントの配信]** セクションで、該当する配信形式メニュー (**[INSERT 配信形式]**、**[UPDATE 配信形式]**、または **[DELETE 配信形式]**) から CALL 構文を選択し、**[INSERT ストアド プロシージャ]**、**[DELETE ストアド プロシージャ]**、または **[UPDATE ストアド プロシージャ]** で使用するプロシージャ名を入力します。 CALL 構文の詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」の「ストアド プロシージャの呼び出し構文」を参照してください。  
  
  
4.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスが表示されている場合は、 **[OK]** をクリックして保存し、ダイアログ ボックスを閉じます。  
  
5.  パブリケーションのスナップショットが生成されると、そのスナップショットには前の手順で指定したプロシージャが含まれています。 このプロシージャは指定した CALL 構文を使用しますが、レプリケーションが使用する既定のロジックを含んでいます。  
  
     スナップショットが生成された後、このアーティクルが属するパブリケーションのスナップショット フォルダーに移動し、アーティクルと同じ名前の **.sch** ファイルを見つけます。 メモ帳などのテキスト エディターでこのファイルを開き、挿入、更新、または削除の各ストアド プロシージャで CREATE PROCEDURE コマンドを検索し、プロシージャ定義を編集してデータの変更を反映するためのカスタム ロジックを指定します。 スナップショットが再生成された場合は、カスタム プロシージャを再作成する必要があります。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
 トランザクション レプリケーションでは、パブリッシャーからサブスクライバーへの変更の反映方法を制御できます。この反映メソッドは、アーティクルの作成時やその後の変更時に、レプリケーションのストアド プロシージャを使用してプログラムから設定できます。  
  
> [!NOTE]  
>  パブリッシュされたデータ行に適用される DML (データ操作言語) 操作には、挿入、更新、削除などがありますが、各種の操作に対して異なる反映メソッドを指定できます。  
  
 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
#### <a name="to-create-an-article-that-uses-transact-sql-commands-to-propagate-data-changes"></a>データ変更を Transact-SQL コマンドを使って反映するアーティクルを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 **\@publication**、 **\@article**、および **\@source_object** に、それぞれ、アーティクルが属しているパブリケーションの名前、アーティクルの名前、および、パブリッシュ対象のデータベース オブジェクトを指定し、さらに、次のパラメーターの少なくとも 1 つに **SQL** を指定します。  
  
    -   **\@ins_cmd** - [INSERT](../../../t-sql/statements/insert-transact-sql.md) コマンドのレプリケーションを制御します。  
  
    -   **\@upd_cmd** - [UPDATE](../../../t-sql/queries/update-transact-sql.md) コマンドのレプリケーションを制御します。  
  
    -   **\@del_cmd** - [DELETE](../../../t-sql/statements/delete-transact-sql.md) コマンドのレプリケーションを制御します。  
  
    > [!NOTE]  
   
  
     詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-create-an-article-that-does-not-propagate-data-changes"></a>データ変更を反映しないアーティクルを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 **\@publication**、 **\@article**、および **\@source_object** に、それぞれ、アーティクルが属しているパブリケーションの名前、アーティクルの名前、および、パブリッシュ対象のデータベース オブジェクトを指定し、さらに、次のパラメーターの少なくとも 1 つに **NONE** を指定します。  
  
    -   **\@ins_cmd** - [INSERT](../../../t-sql/statements/insert-transact-sql.md) コマンドのレプリケーションを制御します。  
  
    -   **\@upd_cmd** - [UPDATE](../../../t-sql/queries/update-transact-sql.md) コマンドのレプリケーションを制御します。  
  
    -   **\@del_cmd** - [DELETE](../../../t-sql/statements/delete-transact-sql.md) コマンドのレプリケーションを制御します。  
  
    > [!NOTE]  
    >  上記のパラメーターに対して **NONE** を指定すると、対応するコマンドはサブスクライバーにレプリケートされません。  
  
     詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
#### <a name="to-create-an-article-with-user-modified-custom-stored-procedures"></a>ユーザーが変更したカスタム ストアド プロシージャを含むアーティクルを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 **\@publication**、 **\@article**、および **\@source_object** に、それぞれ、アーティクルが属しているパブリケーションの名前、アーティクルの名前、および、パブリッシュ対象のデータベース オブジェクトを指定します。さらに、 **\@schema_option** にビットマスク **0x02** (カスタム ストアド プロシージャの自動生成を有効にする) を指定し、次のいずれかのパラメーターを指定します。  
  
    -   **\@ins_cmd** - **CALL sp_MSins_* article_name* ** を指定します。ここで、***article_name*** は **\@article** に指定した値です。  
  
    -   **\@del_cmd** - **CALL sp_MSdel_*article_name*** または **XCALL sp_MSdel_*article_name*** を指定します。ここで、***article_name*** は **\@article** に指定した値です。  
  
    -   **\@upd_cmd** - **SCALL sp_MSupd_* article_name***、**CALL sp_MSupd_* article_name***、**XCALL sp_MSupd_* article_name***、または **MCALL sp_MSupd_* article_name*** を指定します。ここで、***article_name*** は **\@article** に指定した値です。  
  
    > [!NOTE]  
    >  上記コマンド パラメーターのそれぞれについて、レプリケーションによって生成されるストアド プロシージャに独自の名前を指定できます。  
  
    > [!NOTE]  
    >  CALL、SCALL、XCALL、MCALL の各構文の詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
     詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
2.  スナップショットが生成された後、このアーティクルが属するパブリケーションのスナップショット フォルダーに移動し、アーティクルと同じ名前の **.sch** ファイルを見つけます。 このファイルを Notepad.exe で開き、挿入、更新、削除のストアド プロシージャに対応する CREATE PROCEDURE コマンドを見つけ、そのプロシージャ定義を編集して、データ変更を反映するためのカスタム ロジックを指定します。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
#### <a name="to-create-an-article-with-custom-scripting-in-the-custom-stored-procedures-to-propagate-data-changes"></a>カスタム ストアド プロシージャにデータ変更を反映するカスタム スクリプトを含むアーティクルを作成するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)を実行します。 **\@publication**、 **\@article**、および **\@source_object** に、それぞれ、アーティクルが属しているパブリケーションの名前、アーティクルの名前、および、パブリッシュ対象のデータベース オブジェクトを指定します。さらに、 **\@schema_option** にビットマスク **0x02** (カスタム ストアド プロシージャの自動生成を有効にする) を指定し、次のいずれかのパラメーターを指定します。  
  
    -   **\@ins_cmd** - **CALL sp_MSins_* article_name* ** を指定します。ここで、***article_name*** は **\@article** に指定した値です。  
  
    -   **\@del_cmd** - **CALL sp_MSdel_*article_name*** または **XCALL sp_MSdel_* article_name*** を指定します。ここで、***article_name*** は **\@article** に指定した値です。  
  
    -   **\@upd_cmd** - **SCALL sp_MSupd_* article_name* **、**CALL sp_MSupd_* article_name* **、**XCALL sp_MSupd_* article_name* **、**MCALL sp_MSupd_* article_name* ** を指定します。ここで、***article_name*** は **\@article** に指定した値です。  
  
    > [!NOTE]  
    >  上記コマンド パラメーターのそれぞれについて、レプリケーションによって生成されるストアド プロシージャに独自の名前を指定できます。  
  
    > [!NOTE]  
    >  CALL、SCALL、XCALL、MCALL の各構文の詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
     詳しくは、「 [アーティクルを定義](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
2.  パブリッシャーのパブリケーション データベースで、 [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) ステートメントを使用して、挿入、更新、および削除のカスタム ストアド プロシージャに対応する [CREATE PROCEDURE](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) スクリプトが返されるように [sp_scriptpublicationcustomprocs](../../../t-sql/statements/create-procedure-transact-sql.md) を編集します。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
#### <a name="to-change-the-method-of-propagating-changes-for-an-existing-article"></a>既存のアーティクルの変更反映メソッドを変更するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)を実行します。 **\@publication** と **\@article** を指定して、 **\@property** に **ins_cmd**、**upd_cmd**、または **del_cmd** を指定し、さらに、該当する反映メソッドを **\@value** に指定します。  
  
2.  変更対象の各反映メソッドについて、手順 1. を繰り返します。  
  
## <a name="see-also"></a>参照  
 [トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [パブリケーションを作成する](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  
