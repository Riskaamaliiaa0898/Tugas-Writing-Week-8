# React Redux

## Pengertian React Redux

> Redux adalah salah satu state management yang sangat hype pada waktunya dan masih relevan sampai sekarang. Redux juga menawarkan tools untuk masing-masing browser contoh chrome redux devtools untuk memonitor keadaan state kita saat ini.

## Fungsi Redux

> Redux memiliki peran untuk melakukan perubahan state yang dibutuhkan oleh setiap fungsional pada aplikasi. Untuk membuat perubahan tersebut, Redux memiliki tiga komponen utama yaitu action, reducer, dan store.

## Step by Step React Redux - Change Mode

1. Create Project
2. Install package / dependecies yang dibutuhkan :

- redux = $npm install redux
- react-redux = $npm install redux react-redux
- redux-devtools-extension = $npm install --save redux-devtools-extension
- react Router = $react-router-dom@6

**Command install** :
npm install redux react-redux redux-devtools-extension

3. Membuat folder dengan store, didalam folder dibuat lagi 2 folder dan 1 file diantaranya :

- Folder actions
- Folder reducers
- File store.js

4.  Menambahkan 1 file core dengan index.js didalam folder actions

5.  Pada folder actions tambahkan action interface yang dibutuhkan

6.  Menuliskan code pada action interface yang dibutuhkan

        export const changeMode = (data) => {
        return {
        type: "CHANGE_MODE",
        payload: data,
        };
        };

7.  Menambahkan 1 file core dengan index.js didalam filder reducers, lalu import core method combineReducers

        // import combine
        import { combineReducers } from "redux";
        import modeReducer from "./ModeReducer";

        const reducers = combineReducers({
        mode: modeReducer,
        });

        export default reducers;

8.  Pada folder reducers tambahkan file reducer sesuai dengan kebutuhan

        const modeReducer = (state = "light", action) => {
        switch (action.type) {
            case "CHANGE_MODE":
            return action.payload;
            default:
            return state;
        }
        };
        export default modeReducer;

9.  Pada file store.js import core method createStore

        import { createStore } from "redux";
        import reducers from "./reducers";

        const store = createStore(reducers);

        export default store;

10. Pada file index.js yang terdapat di root project src
    import React from "react";
    import ReactDOM from "react-dom/client";
    import "./index.css";
    import App from "./App";
    import reportWebVitals from "./reportWebVitals";

        import { Provider } from "react-redux";
        import store from "./Store/Store";
        import { BrowserRouter } from "react-router-dom";

        const root = ReactDOM.createRoot(document.getElementById("root"));
        root.render(
        <React.StrictMode>
            <Provider store={store}>
            <BrowserRouter>
                <App />
            </BrowserRouter>
            </Provider>
        </React.StrictMode>
        );

# React Testing

## Pengertisn React Testing

> React Testing Library adalah seperangkat helpers yang memungkinkan Anda mengetes komponen pada React tanpa bergantung pada detail implementasinya. Pendekatan ini membuat refactoring menjadi mudah dan juga mendorong Anda untuk menerapkan best practices untuk aksesbilitas.

Ada beberapa cara untuk menguji komponen React. Secara garis besar, mereka dibagi menjadi dua kategori:

1. Merender pohon komponen dalam lingkungan pengujian yang disederhanakan dan menegaskan outputnya.
2. Menjalankan aplikasi lengkap dalam lingkungan browser yang realistis (juga dikenal sebagai pengujian "end-to-end").

# React Context

## Pengertian react Context

> Context menyediakan cara untuk oper data melalui diagram komponen tanpa harus oper props secara manual di setiap tingkat.

> Dalam aplikasi React yang khusus, data dioper dari atas ke bawah (parent ke child) melalui props, tetapi ini bisa menjadi rumit untuk tipe props tertentu (mis. preferensi locale, tema UI) yang dibutuhkan oleh banyak komponen di dalam sebuah aplikasi. Context menyediakan cara untuk berbagi nilai seperti ini di antara komponen tanpa harus oper prop secara explisit melalui setiap tingkatan diagram.

### Kapan Menggunakan Context

> Context dirancang untuk berbagi data yang dapat dianggap “global” untuk diagram komponen React, seperti pengguna terotentikasi saat ini, tema, atau bahasa yang disukai. Misalnya, dalam kode di bawah ini kita secara manual memasang prop “theme” untuk memberi style pada komponen Button:

    class App extends React.Component {
    render() {
        return <Toolbar theme="dark" />;
    }
    }

    function Toolbar(props) {
    // komponen Toolbar harus menggunakan *prop* "theme" tambahan
    // dan oper ke ThemedButton. Ini bisa menjadi *painful*
    // jika setiap tombol di dalam aplikasi perlu mengetahui *theme*-nya
    // karena itu harus melewati semua komponen.
    return (
        <div>
        <ThemedButton theme={props.theme} />
        </div>
    );
    }

    class ThemedButton extends React.Component {
    render() {
        return <Button theme={this.props.theme} />;
    }
    }

### Sebelum Anda Menggunakan Context

> Context terutama digunakan ketika beberapa data harus dapat diakses oleh banyak komponen pada tingkat bersarang yang berbeda. Gunakan dengan hemat karena membuat penggunaan kembali komponen menjadi lebih sulit.

> Jika Anda hanya ingin menghindari mengoper beberapa props melalui banyak tingkatan, komposisi komponen seringkali menjadi solusi yang lebih sederhana daripada context.

> Misalnya, pertimbangkan komponen Page yang mengoper prop user dan avatarSize beberapa tingkat ke bawah sehingga komponen Link dan Avatar yang bersarang dapat membaca prop-nya:

        <Page user={user} avatarSize={avatarSize} />
        // ... yang *render* ...
        <PageLayout user={user} avatarSize={avatarSize} />
        // ... yang *render* ...
        <NavigationBar user={user} avatarSize={avatarSize} />
        // ... yang *render* ...
        <Link href={user.permalink}>
        <Avatar user={user} size={avatarSize} />
        </Link>
