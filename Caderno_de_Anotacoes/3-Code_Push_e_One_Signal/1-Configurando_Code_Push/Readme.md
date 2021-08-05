# Configurando o Code Push

A ferramenta Code Push serve pra facilitar a atualização do app qnd já estiver
em produção e também em ambiente `staging` (tem mais a frente o q é staging),
sem ter q enviar uma nova versão pra loja de aplicativo.

Se o app tiver o código editado sem q tenha q inserir uma lib nativa q tenha q
linkar, o app será atualizado no momento q o usuário o abre.

Instale o `react-native-code-push` no projeto:

`yarn add react-native-code-push`

Linke-o:

`react-native link react-native-code-push`

## src/index.js

O `CheckFrequency` possui 3 opções:

- MANUAL
- ON_APP_RESUME
- ON_APP_START

As opções `Manual`e `ON_APP_RESUME` são melhores. ON_APP_RESUME significa q se
o usuário ficar mais de 10 segundos sem mexer no app, ele atualiza.

A opção `ON_APP_START` não é boa pq depois q atualiza, o app volta pro início.
Daí se o usuário já tiver mexido, ele perde o q fez.

```diff
import React from 'react';
import { StatusBar } from 'react-native';
+import CodePush from 'react-native-code-push';
import { Provider } from 'react-redux';

import { PersistGate } from 'redux-persist/integration/react';

// eslint-disable-next-line import-helpers/order-imports
import App from './App';
import './config/ReactotronConfig';

import { store, persistor } from './store';

const Index = () => (
  <Provider store={store}>
    {/* PersistGate pega o estado antes de renderizar o q tem dentro */}
    <PersistGate persistor={persistor}>
      <StatusBar barStyle="light-content" backgroundColor="#7159c1" />
      <App />
    </PersistGate>
  </Provider>
);

-export default Index;
+export default CodePush({
+  checkFrequency: CodePush.CheckFrequency.ON_APP_RESUME,
+})(Index);
```
