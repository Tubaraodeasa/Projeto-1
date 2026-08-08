# Projeto Android Saint Leo

## TaskFlow - Android application for managing daily tasks and reminders.

### Descrição do projeto
TaskFlow é um aplicativo Android desenvolvido para auxiliar colaboradores no gerenciamento de tarefas diárias, lembretes e eventos importantes da empresa.

### Problema que o aplicativo pretende resolver
Muitas pequenas empresas utilizam anotações em papel ou aplicativos de mensagens para controlar atividades internas, o que pode causar esquecimentos, perda de informações e baixa produtividade. O aplicativo centraliza essas informações em uma única plataforma.

### Plataforma escolhida
Android

### Interface do usuário (UI)
Os colaboradores terão acesso a uma interface simples e intuitiva para visualizar tarefas, eventos, lembretes e notificações.

### Interface do administrador
O administrador poderá cadastrar tarefas, criar eventos, enviar comunicados e acompanhar as atividades dos colaboradores.

### Principais funcionalidades do aplicativo
* Lista de tarefas diárias;
* Calendário de eventos;
* Lembretes com notificações;
* Avisos importantes da empresa;
* Marcação de tarefas concluídas;
* Interface simples e responsiva.

### Design
* Interface minimalista;
* Paleta de cores azul e branca;
* Ícones intuitivos;
* Navegação simples por abas;
* Layout otimizado para smartphones Android.

Módulo 5 — Persistência de dados

Nesta etapa o TaskFlow deixou de guardar as tarefas apenas em memória e passou a persisti-las de fato, usando os mecanismos de armazenamento estudados no módulo. A tela de login agora salva o nome do usuário e o horário do último acesso em um arquivo de SharedPreferences chamado TaskFlowPrefs, aberto com getSharedPreferences(); a MainActivity lê esse mesmo arquivo para exibir a saudação e o último login, mostrando como duas Activities compartilham dados simples sem precisar trocar tudo por Intent. A lista de tarefas, que antes vinha de uma lista mock dentro do TaskViewModel, agora é lida e gravada em um banco SQLite através da nova classe TaskDbHelper, que estende SQLiteOpenHelper e concentra as operações de inserir, atualizar, excluir e listar tarefas na tabela tasks.

A tela de configurações ganhou três novas ações de backup. A primeira exporta todas as tarefas para um arquivo de texto no armazenamento interno do próprio aplicativo, usando openFileOutput() e FileOutputStream; a segunda lê esse mesmo arquivo com openFileInput(), FileInputStream e InputStreamReader para restaurar as tarefas salvas anteriormente. A terceira ação salva uma cópia desse backup fora da área privada do app, na pasta TaskFlow dentro do armazenamento externo, obtida por getExternalStorageDirectory(); como esse método é depreciado a partir do Android 10, o Manifest declara requestLegacyExternalStorage="true" e as permissões de armazenamento com maxSdkVersion, seguindo o mesmo espírito da observação já feita sobre o ListFragment: usar a API pedida pela atividade, mas deixando comentado no código por que ela não é mais a abordagem recomendada. Por fim, a tela de configurações também apresenta uma seção "Sobre o TaskFlow", cujo texto institucional é lido de um arquivo em res/raw através de openRawResource(), e dois switches (notificações e tema escuro) que já são salvos automaticamente pelo framework de Preferences em cima de SharedPreferences.
