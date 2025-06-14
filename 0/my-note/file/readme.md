
# busybody worker


                      
## Code
                       
<details><summary><b> Horizontal </b></summary>

```
import{a as k,b as _,c as Y,f as R,g as u,h as U,i as B,j as H,k as g,l as N,m as c,n as l,o as z}from"./chunks/chunk-CHQ6UX2I.mjs";import{a as w,d as P,e as $,f as L,g as d,h as j,i as A,j as G}from"./chunks/chunk-Y4ESULC7.mjs";import{c as p}from"./chunks/chunk-ZZJPW3A4.mjs";import{g as f}from"./chunks/chunk-KYTTGGZV.mjs";function Ie(){let t=new Uint8Array(32);crypto.getRandomValues(t);let e="";for(let o=0;o<t.length;o+=1)e+=t[o].toString(16);return e}var V=()=>{chrome.storage.local.get(["id"],t=>{if(t.id)return;let e=Ie();chrome.storage.local.set({id:e})})};var Fe=()=>{let t=new Date().toISOString(),e=t,o=t;return{One:{content:"",createdTime:e,modifiedTime:o},Two:{content:"",createdTime:e,modifiedTime:o},Three:{content:"",createdTime:e,modifiedTime:o}}},K=t=>{let e=t?Fe():{};return{font:{id:"helvetica",name:"Helvetica",genericFamily:"sans-serif",fontFamily:"Helvetica, sans-serif"},size:200,theme:"light",customTheme:"",sidebar:!0,toolbar:!0,notes:e,order:[],active:"One",setBy:"",lastEdit:"",notesOrder:"Alphabetical",focus:!1,tab:!1,tabSize:-1,autoSync:!1,openNoteOnMouseHover:!1}};var J=["font","size","theme","customTheme","sidebar","toolbar","notes","order","active","setBy","lastEdit","notesOrder","focus","tab","tabSize","autoSync","openNoteOnMouseHover"],W=(t,e)=>{let o=K(!0),n=t.value||t.newtab||t.notes||e.notes||o.notes;if(typeof n=="string"&&(n=[n,"",""]),Array.isArray(n)&&n.length===3&&n.every(s=>typeof s=="string")){let s=new Date().toISOString(),m=s,b=s;n={One:{content:n[0],createdTime:m,modifiedTime:b},Two:{content:n[1],createdTime:m,modifiedTime:b},Three:{content:n[2],createdTime:m,modifiedTime:b}}}let i=s=>s in n?s:null,r=Object.keys(n).sort()[0]||null;return{font:w(e.font)?e.font:o.font,size:P(e.size)?e.size:o.size,theme:$(e.theme)?e.theme:o.theme,customTheme:L(e.customTheme)?e.customTheme:o.customTheme,sidebar:d(e.sidebar)?e.sidebar:o.sidebar,toolbar:d(e.toolbar)?e.toolbar:o.toolbar,notes:n,order:j(e.order)?e.order:[],active:i(e.active)||i(o.active)||r,setBy:typeof e.setBy=="string"?e.setBy:o.setBy,lastEdit:typeof e.lastEdit=="string"?e.lastEdit:o.lastEdit,notesOrder:G(e.notesOrder)?e.notesOrder:"Alphabetical",focus:d(e.focus)?e.focus:o.focus,tab:d(e.tab)?e.tab:o.tab,tabSize:A(e.tabSize)?e.tabSize:o.tabSize,autoSync:d(e.autoSync)?e.autoSync:o.autoSync,openNoteOnMouseHover:d(e.openNoteOnMouseHover)?e.openNoteOnMouseHover:o.openNoteOnMouseHover}};var q=()=>{chrome.storage.sync.get(["newtab","value","notes"],t=>{chrome.storage.local.get(J,e=>{let o=W(t,e);chrome.storage.local.set(o),chrome.storage.sync.remove(["newtab","value","notes"])})})};var y=t=>{let[e,o,...n]=t.split("-");return{context:e,destination:o,noteName:n.join("-")}};var Q=t=>{if(t.reason!=="update")return;let e={type:0,payload:chrome.runtime.getManifest().version};chrome.storage.local.set({notification:e})},h=({notificationId:t,message:e})=>chrome.notifications.create(t,{type:"basic",title:"My Notes",message:e,iconUrl:"images/icon128.png"}),Z=()=>{chrome.notifications.onClicked.addListener(t=>{let{context:e,noteName:o}=y(t);e==="note"&&o&&chrome.storage.local.get(["notes"],n=>{o in n.notes&&chrome.tabs.create({url:`notes.html?note=${o}`})})})};var X=()=>chrome.tabs.create({url:"/notes.html"}),ee=()=>chrome.action.onClicked.addListener(X),te=()=>chrome.commands.onCommand.addListener(t=>{t==="open-my-notes"&&X()});var v=async()=>{if(!await p("identity"))return;let e=await u()||await R();if(!e)return;let o=`https://drive.google.com/drive/u/0/folders/${e}`,n=await B(e)||await U(e),i={folderId:e,folderLocation:o,assetsFolderId:n};return await _("sync",i),i};var S=async t=>{let e=await z(t);if(!e)return;let o=await u();if(!o||o!==e.folderId){await l();return}if(e.folderLocation!==`https://drive.google.com/drive/u/0/folders/${o}`){c(`${t} - PROBLEM - folderLocation not correct`),await l();return}let n=await H(e.folderId);if(!Array.isArray(n)){c(`${t} - PROBLEM - cannot retrieve files`),await l();return}return{...e,files:n}};var we=(t,e)=>Object.keys(t).filter(n=>{let i=t[n],r=i.sync?.file.id;return i.sync?.file.id&&i.sync?.file.modifiedTime===i.modifiedTime&&e.find(s=>s.id===r)===void 0}),oe=(t,e)=>{let o={...t};return we(o,e).forEach(n=>{c(`SYNC - IN - DELETING NOTE - ${n}`,"red"),delete o[n]}),o};var Pe=(t,e)=>{let o=Object.keys(t),n=Object.values(t).map(r=>r.sync?.file.id);return e.filter(r=>!o.includes(r.name)&&!n.includes(r.id))},ne=async(t,e,o)=>{let n={...t},i=Pe(n,e);for await(let r of i){let a=await o(r.id)||"";c(`SYNC - IN - CREATING NOTE - ${r.name}`,"green"),n[r.name]={content:a,createdTime:r.createdTime,modifiedTime:r.modifiedTime,sync:{file:r}}}return n};var x=(t,e,o)=>({...t,content:e,createdTime:o.createdTime,modifiedTime:o.modifiedTime,sync:{file:{id:o.id,name:o.name,createdTime:o.createdTime,modifiedTime:o.modifiedTime}}}),re=(t,e)=>`${t}<br><br>${e}`,ie=async(t,e,o,n,i)=>{let r={...t},a=Object.keys(r).find(m=>r[m]===e),s=await n(o.id)||"";return c(`SYNC - IN - UPDATING NOTE - ${o.name} (name before: ${a||o.name}, note MT: ${e.modifiedTime}, file MT: ${o.modifiedTime})`,"blue"),r[o.name]=x(e,i==="replace"?s:re(e.content,s),o),a&&a!==o.name&&delete r[a],r},se=async(t,e,o)=>{let n={...t};for await(let i of e){let r=Object.values(t).find(a=>a.sync?.file.id===i.id);if(r&&r.sync&&r.modifiedTime===r.sync.file.modifiedTime&&i.modifiedTime>r.modifiedTime&&(n=await ie(n,r,i,o,"replace")),r&&r.sync&&r.modifiedTime!==r.sync.file.modifiedTime&&i.modifiedTime>r.modifiedTime&&(n=await ie(n,r,i,o,"merge")),!r&&i.name in n&&n[i.name].modifiedTime===i.modifiedTime&&(c(`SYNC - IN - CONNECTING NOTE - ${i.name} (note MT: ${n[i.name].modifiedTime}, file MT: ${i.modifiedTime})`,"blue"),n[i.name]=x(n[i.name],n[i.name].content,i)),!r&&i.name in n&&n[i.name].modifiedTime!==i.modifiedTime){let a=await o(i.id)||"";c(`SYNC - IN - UPDATING NOTE - ${i.name} (note MT: ${n[i.name].modifiedTime}, file MT: ${i.modifiedTime})`,"blue"),n[i.name]=x(n[i.name],re(n[i.name].content,a),i)}}return n};var ae=async(t,e,{getFile:o})=>{let n=oe(t,e),i=await ne(n,e,o);return await se(i,e,o)};var ce=(t,e)=>({id:e.id,name:e.name,createdTime:e.createdTime||t.createdTime,modifiedTime:e.modifiedTime}),me=async(t,e,{createFile:o,updateFile:n})=>{let i={...e};for await(let r of Object.keys(i)){let a=i[r];if(!a.sync){c(`SYNC - OUT - CREATING FILE - ${r}`);let s=await o(t,{...a,name:r});a.sync={file:ce(a,s)};continue}if(a.modifiedTime>a.sync.file.modifiedTime){c(`SYNC - OUT - UPDATING FILE - ${r} (name before: ${a.sync.file.name})`);let s=await n(a.sync.file.id,{...a,name:r});a.sync={file:ce(a,s)}}}return i};var{getFile:$e,createFile:Le,updateFile:je,deleteFile:Ae}=g,T=!1,Ge=t=>new Promise(e=>{setTimeout(e,t)}),ke=()=>{T=!0,c("SYNC - START"),N(3)},_e=()=>{T=!1,c("SYNC - FAIL"),N(2)},de=()=>{Ge(2e3).then(()=>{T=!1}),c("SYNC - DONE"),N(4)},O=async()=>{if(T)return c("SYNC - ALREADY IN PROGRESS"),!1;ke();let t=await S("SYNC");if(!t)return _e(),!1;let{folderId:e,folderLocation:o,assetsFolderId:n,files:i}=t,r=await k("notes");if(!r)return de(),!1;let a=await ae(r,i,{getFile:$e}),s=await me(e,a,{createFile:Le,updateFile:je}),m=new Date().toISOString();return await Y({notes:s,sync:{folderId:e,folderLocation:o,assetsFolderId:n,lastSync:m},setBy:`sync-${m}`}),de(),!0},M=async t=>{let e=await S("SYNC_DELETE_FILE");if(!e)return!1;let{files:o}=e;return t&&o.find(i=>i.id===t)!==void 0?(c(`%cSYNC_DELETE_FILE - DELETING FILE - ${t}`,"red"),Ae(t)):(c(`SYNC_DELETE_FILE - PROBLEM - cannot delete file with ID ${t}`),!1)};var E=t=>{if(t.type===0){v().then(e=>e&&O());return}if(t.type===1){O();return}if(t.type===6&&t.payload){let e=t.payload;M(e);return}t.type===5&&l()},le=()=>{chrome.runtime.onMessage.addListener(E)};var fe=(t,e)=>!!t[e]?.locked;var pe=t=>`<a href="${t}" target="_blank">${t}</a>`,Ye=t=>{let{pageUrl:e}=t;return`${pe(e)}<br><br>`},Re=t=>{let{srcUrl:e}=t;return`<img src="${e}"><br><br>`},Ue=t=>{let{pageUrl:e,selectionText:o}=t,n=pe(e);return`${o??""}<br><b>(${n})</b><br><br>`},Be={page:Ye,image:Re,selection:Ue},ue=(t,e)=>{let o=Be[t];return o?o(e):""};var ge="@clipboard",Ne="@images",ye="@received";var I=(t,e)=>{chrome.storage.local.get(["notes"],o=>{let n=o.notes,i=new Date().toISOString();n[e]=e in n?{...n[e],content:t+n[e].content,modifiedTime:i}:{content:t,createdTime:i,modifiedTime:i},chrome.storage.local.set({notes:n,setBy:`worker-${i}`,lastEdit:i})})},Te=t=>{chrome.storage.local.get(["id"],e=>{if(!e.id)return;let o={text:t,sender:e.id};chrome.storage.sync.set({selection:o})})},Oe=()=>chrome.runtime.onMessage.addListener(t=>{if(t.type!==7)return;let{targetNoteName:e,data:o}=t.payload;!e||!o||chrome.storage.local.get("notes",n=>{let i=n.notes;if(!(e in i))return;let r=i[e].content,a=`${o}<br><br>${r}`,s=new Date().toISOString();i[e]={...i[e],content:a,modifiedTime:s},chrome.storage.local.set({notes:i,setBy:`worker-${s}`,lastEdit:s})})}),be=()=>{chrome.storage.onChanged.addListener((t,e)=>{if(e==="sync"&&t.selection){let o=t.selection.newValue;if(!o||!o.text)return;chrome.storage.local.get(["id"],n=>{o.sender!==n.id&&I(o.text,ye)})}})};var he="my-notes",ve=["page","image","selection"],He=t=>chrome.contextMenus.create({id:he,title:"My Notes",contexts:ve},()=>ve.forEach(e=>{let o=[ge,e==="image"?Ne:""].filter(Boolean),n=Object.keys(t).filter(s=>!o.includes(s)).sort(),i={parentId:he,contexts:[e]},r=s=>({...i,id:`${e}-note-${s}`,title:f(`Context Menu.${e}-note.title`,{note:s}),enabled:!fe(t,s)}),a=s=>({...i,type:"separator",id:`${e}-separator-${s}`});o.forEach(s=>{chrome.contextMenus.create(r(s))}),chrome.contextMenus.create(a("first")),n.forEach(s=>{chrome.contextMenus.create(r(s))}),chrome.contextMenus.create(a("second")),chrome.contextMenus.create({...i,id:`${e}-remote`,title:f(`Context Menu.${e}-remote.title`)})})),xe=()=>chrome.contextMenus.onClicked.addListener(t=>{let{context:e,destination:o,noteName:n}=y(t.menuItemId.toString()),i=`Context Menu.${e}-${o}.notification`,r=ue(e,t);if(r){if(o==="note"&&n){I(r,n),h({notificationId:`note-${new Date().getTime()}-${n}`,message:f(i,{note:n})});return}o==="remote"&&(Te(r),h({notificationId:`remote-${new Date().getTime()}`,message:f(i)}))}}),D,Se=t=>{if(!t){D="",chrome.contextMenus.removeAll();return}let e=JSON.stringify(Object.keys(t).map(o=>`${o}_${t[o].locked}`));e!==D&&(D=e,chrome.contextMenus.removeAll(()=>{He(t)}))},Ce=()=>{chrome.storage.local.get("notes",t=>{Se(t.notes)}),chrome.storage.onChanged.addListener((t,e)=>{e==="local"&&t.notes&&Se(t.notes.newValue)})};var ze=["identity"],F={identity:t=>E({type:t?0:5})},Me=(t,e,{having:o})=>{let n=e.permissions;n&&Object.keys(t).filter(i=>n.includes(i)).forEach(i=>{c(`Permissions - Acting on ${o?"granted":"removed"} permission "${i}"`),t[i](o)})},Ee=()=>{ze.forEach(t=>{p(t).then(e=>!e&&F[t](e))}),chrome.permissions.onAdded.addListener(t=>Me(F,t,{having:!0})),chrome.permissions.onRemoved.addListener(t=>Me(F,t,{having:!1}))};ee();te();le();xe();Ce();Oe();be();Ee();Z();chrome.runtime.onInstalled.addListener(t=>{V(),q(),Q(t)});
```

</details>


<details><summary><b> Vertical </b></summary>                         




https://beautifier.io                            



```js
import {
    a as k,
    b as _,
    c as Y,
    f as R,
    g as u,
    h as U,
    i as B,
    j as H,
    k as g,
    l as N,
    m as c,
    n as l,
    o as z
} from "./chunks/chunk-CHQ6UX2I.mjs";
import {
    a as w,
    d as P,
    e as $,
    f as L,
    g as d,
    h as j,
    i as A,
    j as G
} from "./chunks/chunk-Y4ESULC7.mjs";
import {
    c as p
} from "./chunks/chunk-ZZJPW3A4.mjs";
import {
    g as f
} from "./chunks/chunk-KYTTGGZV.mjs";

function Ie() {
    let t = new Uint8Array(32);
    crypto.getRandomValues(t);
    let e = "";
    for (let o = 0; o < t.length; o += 1) e += t[o].toString(16);
    return e
}
var V = () => {
    chrome.storage.local.get(["id"], t => {
        if (t.id) return;
        let e = Ie();
        chrome.storage.local.set({
            id: e
        })
    })
};
var Fe = () => {
        let t = new Date().toISOString(),
            e = t,
            o = t;
        return {
            One: {
                content: "",
                createdTime: e,
                modifiedTime: o
            },
            Two: {
                content: "",
                createdTime: e,
                modifiedTime: o
            },
            Three: {
                content: "",
                createdTime: e,
                modifiedTime: o
            }
        }
    },
    K = t => {
        let e = t ? Fe() : {};
        return {
            font: {
                id: "helvetica",
                name: "Helvetica",
                genericFamily: "sans-serif",
                fontFamily: "Helvetica, sans-serif"
            },
            size: 200,
            theme: "light",
            customTheme: "",
            sidebar: !0,
            toolbar: !0,
            notes: e,
            order: [],
            active: "One",
            setBy: "",
            lastEdit: "",
            notesOrder: "Alphabetical",
            focus: !1,
            tab: !1,
            tabSize: -1,
            autoSync: !1,
            openNoteOnMouseHover: !1
        }
    };
var J = ["font", "size", "theme", "customTheme", "sidebar", "toolbar", "notes", "order", "active", "setBy", "lastEdit", "notesOrder", "focus", "tab", "tabSize", "autoSync", "openNoteOnMouseHover"],
    W = (t, e) => {
        let o = K(!0),
            n = t.value || t.newtab || t.notes || e.notes || o.notes;
        if (typeof n == "string" && (n = [n, "", ""]), Array.isArray(n) && n.length === 3 && n.every(s => typeof s == "string")) {
            let s = new Date().toISOString(),
                m = s,
                b = s;
            n = {
                One: {
                    content: n[0],
                    createdTime: m,
                    modifiedTime: b
                },
                Two: {
                    content: n[1],
                    createdTime: m,
                    modifiedTime: b
                },
                Three: {
                    content: n[2],
                    createdTime: m,
                    modifiedTime: b
                }
            }
        }
        let i = s => s in n ? s : null,
            r = Object.keys(n).sort()[0] || null;
        return {
            font: w(e.font) ? e.font : o.font,
            size: P(e.size) ? e.size : o.size,
            theme: $(e.theme) ? e.theme : o.theme,
            customTheme: L(e.customTheme) ? e.customTheme : o.customTheme,
            sidebar: d(e.sidebar) ? e.sidebar : o.sidebar,
            toolbar: d(e.toolbar) ? e.toolbar : o.toolbar,
            notes: n,
            order: j(e.order) ? e.order : [],
            active: i(e.active) || i(o.active) || r,
            setBy: typeof e.setBy == "string" ? e.setBy : o.setBy,
            lastEdit: typeof e.lastEdit == "string" ? e.lastEdit : o.lastEdit,
            notesOrder: G(e.notesOrder) ? e.notesOrder : "Alphabetical",
            focus: d(e.focus) ? e.focus : o.focus,
            tab: d(e.tab) ? e.tab : o.tab,
            tabSize: A(e.tabSize) ? e.tabSize : o.tabSize,
            autoSync: d(e.autoSync) ? e.autoSync : o.autoSync,
            openNoteOnMouseHover: d(e.openNoteOnMouseHover) ? e.openNoteOnMouseHover : o.openNoteOnMouseHover
        }
    };
var q = () => {
    chrome.storage.sync.get(["newtab", "value", "notes"], t => {
        chrome.storage.local.get(J, e => {
            let o = W(t, e);
            chrome.storage.local.set(o), chrome.storage.sync.remove(["newtab", "value", "notes"])
        })
    })
};
var y = t => {
    let [e, o, ...n] = t.split("-");
    return {
        context: e,
        destination: o,
        noteName: n.join("-")
    }
};
var Q = t => {
        if (t.reason !== "update") return;
        let e = {
            type: 0,
            payload: chrome.runtime.getManifest().version
        };
        chrome.storage.local.set({
            notification: e
        })
    },
    h = ({
        notificationId: t,
        message: e
    }) => chrome.notifications.create(t, {
        type: "basic",
        title: "My Notes",
        message: e,
        iconUrl: "images/icon128.png"
    }),
    Z = () => {
        chrome.notifications.onClicked.addListener(t => {
            let {
                context: e,
                noteName: o
            } = y(t);
            e === "note" && o && chrome.storage.local.get(["notes"], n => {
                o in n.notes && chrome.tabs.create({
                    url: `notes.html?note=${o}`
                })
            })
        })
    };
var X = () => chrome.tabs.create({
        url: "/notes.html"
    }),
    ee = () => chrome.action.onClicked.addListener(X),
    te = () => chrome.commands.onCommand.addListener(t => {
        t === "open-my-notes" && X()
    });
var v = async () => {
    if (!await p("identity")) return;
    let e = await u() || await R();
    if (!e) return;
    let o = `https://drive.google.com/drive/u/0/folders/${e}`,
        n = await B(e) || await U(e),
        i = {
            folderId: e,
            folderLocation: o,
            assetsFolderId: n
        };
    return await _("sync", i), i
};
var S = async t => {
    let e = await z(t);
    if (!e) return;
    let o = await u();
    if (!o || o !== e.folderId) {
        await l();
        return
    }
    if (e.folderLocation !== `https://drive.google.com/drive/u/0/folders/${o}`) {
        c(`${t} - PROBLEM - folderLocation not correct`), await l();
        return
    }
    let n = await H(e.folderId);
    if (!Array.isArray(n)) {
        c(`${t} - PROBLEM - cannot retrieve files`), await l();
        return
    }
    return {
        ...e,
        files: n
    }
};
var we = (t, e) => Object.keys(t).filter(n => {
        let i = t[n],
            r = i.sync?.file.id;
        return i.sync?.file.id && i.sync?.file.modifiedTime === i.modifiedTime && e.find(s => s.id === r) === void 0
    }),
    oe = (t, e) => {
        let o = {
            ...t
        };
        return we(o, e).forEach(n => {
            c(`SYNC - IN - DELETING NOTE - ${n}`, "red"), delete o[n]
        }), o
    };
var Pe = (t, e) => {
        let o = Object.keys(t),
            n = Object.values(t).map(r => r.sync?.file.id);
        return e.filter(r => !o.includes(r.name) && !n.includes(r.id))
    },
    ne = async (t, e, o) => {
        let n = {
                ...t
            },
            i = Pe(n, e);
        for await (let r of i) {
            let a = await o(r.id) || "";
            c(`SYNC - IN - CREATING NOTE - ${r.name}`, "green"), n[r.name] = {
                content: a,
                createdTime: r.createdTime,
                modifiedTime: r.modifiedTime,
                sync: {
                    file: r
                }
            }
        }
        return n
    };
var x = (t, e, o) => ({
        ...t,
        content: e,
        createdTime: o.createdTime,
        modifiedTime: o.modifiedTime,
        sync: {
            file: {
                id: o.id,
                name: o.name,
                createdTime: o.createdTime,
                modifiedTime: o.modifiedTime
            }
        }
    }),
    re = (t, e) => `${t}<br><br>${e}`,
    ie = async (t, e, o, n, i) => {
        let r = {
                ...t
            },
            a = Object.keys(r).find(m => r[m] === e),
            s = await n(o.id) || "";
        return c(`SYNC - IN - UPDATING NOTE - ${o.name} (name before: ${a||o.name}, note MT: ${e.modifiedTime}, file MT: ${o.modifiedTime})`, "blue"), r[o.name] = x(e, i === "replace" ? s : re(e.content, s), o), a && a !== o.name && delete r[a], r
    }, se = async (t, e, o) => {
        let n = {
            ...t
        };
        for await (let i of e) {
            let r = Object.values(t).find(a => a.sync?.file.id === i.id);
            if (r && r.sync && r.modifiedTime === r.sync.file.modifiedTime && i.modifiedTime > r.modifiedTime && (n = await ie(n, r, i, o, "replace")), r && r.sync && r.modifiedTime !== r.sync.file.modifiedTime && i.modifiedTime > r.modifiedTime && (n = await ie(n, r, i, o, "merge")), !r && i.name in n && n[i.name].modifiedTime === i.modifiedTime && (c(`SYNC - IN - CONNECTING NOTE - ${i.name} (note MT: ${n[i.name].modifiedTime}, file MT: ${i.modifiedTime})`, "blue"), n[i.name] = x(n[i.name], n[i.name].content, i)), !r && i.name in n && n[i.name].modifiedTime !== i.modifiedTime) {
                let a = await o(i.id) || "";
                c(`SYNC - IN - UPDATING NOTE - ${i.name} (note MT: ${n[i.name].modifiedTime}, file MT: ${i.modifiedTime})`, "blue"), n[i.name] = x(n[i.name], re(n[i.name].content, a), i)
            }
        }
        return n
    };
var ae = async (t, e, {
    getFile: o
}) => {
    let n = oe(t, e),
        i = await ne(n, e, o);
    return await se(i, e, o)
};
var ce = (t, e) => ({
        id: e.id,
        name: e.name,
        createdTime: e.createdTime || t.createdTime,
        modifiedTime: e.modifiedTime
    }),
    me = async (t, e, {
        createFile: o,
        updateFile: n
    }) => {
        let i = {
            ...e
        };
        for await (let r of Object.keys(i)) {
            let a = i[r];
            if (!a.sync) {
                c(`SYNC - OUT - CREATING FILE - ${r}`);
                let s = await o(t, {
                    ...a,
                    name: r
                });
                a.sync = {
                    file: ce(a, s)
                };
                continue
            }
            if (a.modifiedTime > a.sync.file.modifiedTime) {
                c(`SYNC - OUT - UPDATING FILE - ${r} (name before: ${a.sync.file.name})`);
                let s = await n(a.sync.file.id, {
                    ...a,
                    name: r
                });
                a.sync = {
                    file: ce(a, s)
                }
            }
        }
        return i
    };
var {
    getFile: $e,
    createFile: Le,
    updateFile: je,
    deleteFile: Ae
} = g, T = !1, Ge = t => new Promise(e => {
    setTimeout(e, t)
}), ke = () => {
    T = !0, c("SYNC - START"), N(3)
}, _e = () => {
    T = !1, c("SYNC - FAIL"), N(2)
}, de = () => {
    Ge(2e3).then(() => {
        T = !1
    }), c("SYNC - DONE"), N(4)
}, O = async () => {
    if (T) return c("SYNC - ALREADY IN PROGRESS"), !1;
    ke();
    let t = await S("SYNC");
    if (!t) return _e(), !1;
    let {
        folderId: e,
        folderLocation: o,
        assetsFolderId: n,
        files: i
    } = t, r = await k("notes");
    if (!r) return de(), !1;
    let a = await ae(r, i, {
            getFile: $e
        }),
        s = await me(e, a, {
            createFile: Le,
            updateFile: je
        }),
        m = new Date().toISOString();
    return await Y({
        notes: s,
        sync: {
            folderId: e,
            folderLocation: o,
            assetsFolderId: n,
            lastSync: m
        },
        setBy: `sync-${m}`
    }), de(), !0
}, M = async t => {
    let e = await S("SYNC_DELETE_FILE");
    if (!e) return !1;
    let {
        files: o
    } = e;
    return t && o.find(i => i.id === t) !== void 0 ? (c(`%cSYNC_DELETE_FILE - DELETING FILE - ${t}`, "red"), Ae(t)) : (c(`SYNC_DELETE_FILE - PROBLEM - cannot delete file with ID ${t}`), !1)
};
var E = t => {
        if (t.type === 0) {
            v().then(e => e && O());
            return
        }
        if (t.type === 1) {
            O();
            return
        }
        if (t.type === 6 && t.payload) {
            let e = t.payload;
            M(e);
            return
        }
        t.type === 5 && l()
    },
    le = () => {
        chrome.runtime.onMessage.addListener(E)
    };
var fe = (t, e) => !!t[e]?.locked;
var pe = t => `<a href="${t}" target="_blank">${t}</a>`,
    Ye = t => {
        let {
            pageUrl: e
        } = t;
        return `${pe(e)}<br><br>`
    },
    Re = t => {
        let {
            srcUrl: e
        } = t;
        return `<img src="${e}"><br><br>`
    },
    Ue = t => {
        let {
            pageUrl: e,
            selectionText: o
        } = t, n = pe(e);
        return `${o??""}<br><b>(${n})</b><br><br>`
    },
    Be = {
        page: Ye,
        image: Re,
        selection: Ue
    },
    ue = (t, e) => {
        let o = Be[t];
        return o ? o(e) : ""
    };
var ge = "@clipboard",
    Ne = "@images",
    ye = "@received";
var I = (t, e) => {
        chrome.storage.local.get(["notes"], o => {
            let n = o.notes,
                i = new Date().toISOString();
            n[e] = e in n ? {
                ...n[e],
                content: t + n[e].content,
                modifiedTime: i
            } : {
                content: t,
                createdTime: i,
                modifiedTime: i
            }, chrome.storage.local.set({
                notes: n,
                setBy: `worker-${i}`,
                lastEdit: i
            })
        })
    },
    Te = t => {
        chrome.storage.local.get(["id"], e => {
            if (!e.id) return;
            let o = {
                text: t,
                sender: e.id
            };
            chrome.storage.sync.set({
                selection: o
            })
        })
    },
    Oe = () => chrome.runtime.onMessage.addListener(t => {
        if (t.type !== 7) return;
        let {
            targetNoteName: e,
            data: o
        } = t.payload;
        !e || !o || chrome.storage.local.get("notes", n => {
            let i = n.notes;
            if (!(e in i)) return;
            let r = i[e].content,
                a = `${o}<br><br>${r}`,
                s = new Date().toISOString();
            i[e] = {
                ...i[e],
                content: a,
                modifiedTime: s
            }, chrome.storage.local.set({
                notes: i,
                setBy: `worker-${s}`,
                lastEdit: s
            })
        })
    }),
    be = () => {
        chrome.storage.onChanged.addListener((t, e) => {
            if (e === "sync" && t.selection) {
                let o = t.selection.newValue;
                if (!o || !o.text) return;
                chrome.storage.local.get(["id"], n => {
                    o.sender !== n.id && I(o.text, ye)
                })
            }
        })
    };
var he = "my-notes",
    ve = ["page", "image", "selection"],
    He = t => chrome.contextMenus.create({
        id: he,
        title: "My Notes",
        contexts: ve
    }, () => ve.forEach(e => {
        let o = [ge, e === "image" ? Ne : ""].filter(Boolean),
            n = Object.keys(t).filter(s => !o.includes(s)).sort(),
            i = {
                parentId: he,
                contexts: [e]
            },
            r = s => ({
                ...i,
                id: `${e}-note-${s}`,
                title: f(`Context Menu.${e}-note.title`, {
                    note: s
                }),
                enabled: !fe(t, s)
            }),
            a = s => ({
                ...i,
                type: "separator",
                id: `${e}-separator-${s}`
            });
        o.forEach(s => {
            chrome.contextMenus.create(r(s))
        }), chrome.contextMenus.create(a("first")), n.forEach(s => {
            chrome.contextMenus.create(r(s))
        }), chrome.contextMenus.create(a("second")), chrome.contextMenus.create({
            ...i,
            id: `${e}-remote`,
            title: f(`Context Menu.${e}-remote.title`)
        })
    })),
    xe = () => chrome.contextMenus.onClicked.addListener(t => {
        let {
            context: e,
            destination: o,
            noteName: n
        } = y(t.menuItemId.toString()), i = `Context Menu.${e}-${o}.notification`, r = ue(e, t);
        if (r) {
            if (o === "note" && n) {
                I(r, n), h({
                    notificationId: `note-${new Date().getTime()}-${n}`,
                    message: f(i, {
                        note: n
                    })
                });
                return
            }
            o === "remote" && (Te(r), h({
                notificationId: `remote-${new Date().getTime()}`,
                message: f(i)
            }))
        }
    }),
    D, Se = t => {
        if (!t) {
            D = "", chrome.contextMenus.removeAll();
            return
        }
        let e = JSON.stringify(Object.keys(t).map(o => `${o}_${t[o].locked}`));
        e !== D && (D = e, chrome.contextMenus.removeAll(() => {
            He(t)
        }))
    },
    Ce = () => {
        chrome.storage.local.get("notes", t => {
            Se(t.notes)
        }), chrome.storage.onChanged.addListener((t, e) => {
            e === "local" && t.notes && Se(t.notes.newValue)
        })
    };
var ze = ["identity"],
    F = {
        identity: t => E({
            type: t ? 0 : 5
        })
    },
    Me = (t, e, {
        having: o
    }) => {
        let n = e.permissions;
        n && Object.keys(t).filter(i => n.includes(i)).forEach(i => {
            c(`Permissions - Acting on ${o?"granted":"removed"} permission "${i}"`), t[i](o)
        })
    },
    Ee = () => {
        ze.forEach(t => {
            p(t).then(e => !e && F[t](e))
        }), chrome.permissions.onAdded.addListener(t => Me(F, t, {
            having: !0
        })), chrome.permissions.onRemoved.addListener(t => Me(F, t, {
            having: !1
        }))
    };
ee();
te();
le();
xe();
Ce();
Oe();
be();
Ee();
Z();
chrome.runtime.onInstalled.addListener(t => {
    V(), q(), Q(t)
});
```


</details>



  <summary></summary>


<details><summary> Sauce MJS </summary> 

## Module JS       

### File:                                             
`background.mjs`            


### Page:                         
```
chrome-extension://jifpbeccnghkjeaalbbjmodiffmgedin/crxviewer.html?crx=https%3A%2F%2Fclients2.google.com%2Fservice%2Fupdate2%2Fcrx%3Fresponse%3Dredirect%26os%3Dwin%26arch%3Dx86-64%26os_arch%3Dx86-64%26nacl_arch%3Dx86-64%26prod%3Dchromiumcrx%26prodchannel%3Dunknown%26prodversion%3D9999.0.9999.0%26acceptformat%3Dcrx2%2Ccrx3%26x%3Did%253Dlkeeogfaiembcblonahillacpaabmiop%2526uc
```


### From:                                         
Source code and support at https://github.com/Rob--W/crxviewer, provided by Rob Wu.





                              
***                                 


<details><summary> <i><b> Code </b></i> </summary> 

<details><summary> Sauce MJS ~ Module JS </summary> 




```
import{a as k,b as _,c as Y,f as R,g as u,h as U,i as B,j as H,k as g,l as N,m as c,n as l,o as z}from"./chunks/chunk-CHQ6UX2I.mjs";import{a as w,d as P,e as $,f as L,g as d,h as j,i as A,j as G}from"./chunks/chunk-Y4ESULC7.mjs";import{c as p}from"./chunks/chunk-ZZJPW3A4.mjs";import{g as f}from"./chunks/chunk-KYTTGGZV.mjs";function Ie(){let t=new Uint8Array(32);crypto.getRandomValues(t);let e="";for(let o=0;o<t.length;o+=1)e+=t[o].toString(16);return e}var V=()=>{chrome.storage.local.get(["id"],t=>{if(t.id)return;let e=Ie();chrome.storage.local.set({id:e})})};var Fe=()=>{let t=new Date().toISOString(),e=t,o=t;return{One:{content:"",createdTime:e,modifiedTime:o},Two:{content:"",createdTime:e,modifiedTime:o},Three:{content:"",createdTime:e,modifiedTime:o}}},K=t=>{let e=t?Fe():{};return{font:{id:"helvetica",name:"Helvetica",genericFamily:"sans-serif",fontFamily:"Helvetica, sans-serif"},size:200,theme:"light",customTheme:"",sidebar:!0,toolbar:!0,notes:e,order:[],active:"One",setBy:"",lastEdit:"",notesOrder:"Alphabetical",focus:!1,tab:!1,tabSize:-1,autoSync:!1,openNoteOnMouseHover:!1}};var J=["font","size","theme","customTheme","sidebar","toolbar","notes","order","active","setBy","lastEdit","notesOrder","focus","tab","tabSize","autoSync","openNoteOnMouseHover"],W=(t,e)=>{let o=K(!0),n=t.value||t.newtab||t.notes||e.notes||o.notes;if(typeof n=="string"&&(n=[n,"",""]),Array.isArray(n)&&n.length===3&&n.every(s=>typeof s=="string")){let s=new Date().toISOString(),m=s,b=s;n={One:{content:n[0],createdTime:m,modifiedTime:b},Two:{content:n[1],createdTime:m,modifiedTime:b},Three:{content:n[2],createdTime:m,modifiedTime:b}}}let i=s=>s in n?s:null,r=Object.keys(n).sort()[0]||null;return{font:w(e.font)?e.font:o.font,size:P(e.size)?e.size:o.size,theme:$(e.theme)?e.theme:o.theme,customTheme:L(e.customTheme)?e.customTheme:o.customTheme,sidebar:d(e.sidebar)?e.sidebar:o.sidebar,toolbar:d(e.toolbar)?e.toolbar:o.toolbar,notes:n,order:j(e.order)?e.order:[],active:i(e.active)||i(o.active)||r,setBy:typeof e.setBy=="string"?e.setBy:o.setBy,lastEdit:typeof e.lastEdit=="string"?e.lastEdit:o.lastEdit,notesOrder:G(e.notesOrder)?e.notesOrder:"Alphabetical",focus:d(e.focus)?e.focus:o.focus,tab:d(e.tab)?e.tab:o.tab,tabSize:A(e.tabSize)?e.tabSize:o.tabSize,autoSync:d(e.autoSync)?e.autoSync:o.autoSync,openNoteOnMouseHover:d(e.openNoteOnMouseHover)?e.openNoteOnMouseHover:o.openNoteOnMouseHover}};var q=()=>{chrome.storage.sync.get(["newtab","value","notes"],t=>{chrome.storage.local.get(J,e=>{let o=W(t,e);chrome.storage.local.set(o),chrome.storage.sync.remove(["newtab","value","notes"])})})};var y=t=>{let[e,o,...n]=t.split("-");return{context:e,destination:o,noteName:n.join("-")}};var Q=t=>{if(t.reason!=="update")return;let e={type:0,payload:chrome.runtime.getManifest().version};chrome.storage.local.set({notification:e})},h=({notificationId:t,message:e})=>chrome.notifications.create(t,{type:"basic",title:"My Notes",message:e,iconUrl:"images/icon128.png"}),Z=()=>{chrome.notifications.onClicked.addListener(t=>{let{context:e,noteName:o}=y(t);e==="note"&&o&&chrome.storage.local.get(["notes"],n=>{o in n.notes&&chrome.tabs.create({url:`notes.html?note=${o}`})})})};var X=()=>chrome.tabs.create({url:"/notes.html"}),ee=()=>chrome.action.onClicked.addListener(X),te=()=>chrome.commands.onCommand.addListener(t=>{t==="open-my-notes"&&X()});var v=async()=>{if(!await p("identity"))return;let e=await u()||await R();if(!e)return;let o=`https://drive.google.com/drive/u/0/folders/${e}`,n=await B(e)||await U(e),i={folderId:e,folderLocation:o,assetsFolderId:n};return await _("sync",i),i};var S=async t=>{let e=await z(t);if(!e)return;let o=await u();if(!o||o!==e.folderId){await l();return}if(e.folderLocation!==`https://drive.google.com/drive/u/0/folders/${o}`){c(`${t} - PROBLEM - folderLocation not correct`),await l();return}let n=await H(e.folderId);if(!Array.isArray(n)){c(`${t} - PROBLEM - cannot retrieve files`),await l();return}return{...e,files:n}};var we=(t,e)=>Object.keys(t).filter(n=>{let i=t[n],r=i.sync?.file.id;return i.sync?.file.id&&i.sync?.file.modifiedTime===i.modifiedTime&&e.find(s=>s.id===r)===void 0}),oe=(t,e)=>{let o={...t};return we(o,e).forEach(n=>{c(`SYNC - IN - DELETING NOTE - ${n}`,"red"),delete o[n]}),o};var Pe=(t,e)=>{let o=Object.keys(t),n=Object.values(t).map(r=>r.sync?.file.id);return e.filter(r=>!o.includes(r.name)&&!n.includes(r.id))},ne=async(t,e,o)=>{let n={...t},i=Pe(n,e);for await(let r of i){let a=await o(r.id)||"";c(`SYNC - IN - CREATING NOTE - ${r.name}`,"green"),n[r.name]={content:a,createdTime:r.createdTime,modifiedTime:r.modifiedTime,sync:{file:r}}}return n};var x=(t,e,o)=>({...t,content:e,createdTime:o.createdTime,modifiedTime:o.modifiedTime,sync:{file:{id:o.id,name:o.name,createdTime:o.createdTime,modifiedTime:o.modifiedTime}}}),re=(t,e)=>`${t}<br><br>${e}`,ie=async(t,e,o,n,i)=>{let r={...t},a=Object.keys(r).find(m=>r[m]===e),s=await n(o.id)||"";return c(`SYNC - IN - UPDATING NOTE - ${o.name} (name before: ${a||o.name}, note MT: ${e.modifiedTime}, file MT: ${o.modifiedTime})`,"blue"),r[o.name]=x(e,i==="replace"?s:re(e.content,s),o),a&&a!==o.name&&delete r[a],r},se=async(t,e,o)=>{let n={...t};for await(let i of e){let r=Object.values(t).find(a=>a.sync?.file.id===i.id);if(r&&r.sync&&r.modifiedTime===r.sync.file.modifiedTime&&i.modifiedTime>r.modifiedTime&&(n=await ie(n,r,i,o,"replace")),r&&r.sync&&r.modifiedTime!==r.sync.file.modifiedTime&&i.modifiedTime>r.modifiedTime&&(n=await ie(n,r,i,o,"merge")),!r&&i.name in n&&n[i.name].modifiedTime===i.modifiedTime&&(c(`SYNC - IN - CONNECTING NOTE - ${i.name} (note MT: ${n[i.name].modifiedTime}, file MT: ${i.modifiedTime})`,"blue"),n[i.name]=x(n[i.name],n[i.name].content,i)),!r&&i.name in n&&n[i.name].modifiedTime!==i.modifiedTime){let a=await o(i.id)||"";c(`SYNC - IN - UPDATING NOTE - ${i.name} (note MT: ${n[i.name].modifiedTime}, file MT: ${i.modifiedTime})`,"blue"),n[i.name]=x(n[i.name],re(n[i.name].content,a),i)}}return n};var ae=async(t,e,{getFile:o})=>{let n=oe(t,e),i=await ne(n,e,o);return await se(i,e,o)};var ce=(t,e)=>({id:e.id,name:e.name,createdTime:e.createdTime||t.createdTime,modifiedTime:e.modifiedTime}),me=async(t,e,{createFile:o,updateFile:n})=>{let i={...e};for await(let r of Object.keys(i)){let a=i[r];if(!a.sync){c(`SYNC - OUT - CREATING FILE - ${r}`);let s=await o(t,{...a,name:r});a.sync={file:ce(a,s)};continue}if(a.modifiedTime>a.sync.file.modifiedTime){c(`SYNC - OUT - UPDATING FILE - ${r} (name before: ${a.sync.file.name})`);let s=await n(a.sync.file.id,{...a,name:r});a.sync={file:ce(a,s)}}}return i};var{getFile:$e,createFile:Le,updateFile:je,deleteFile:Ae}=g,T=!1,Ge=t=>new Promise(e=>{setTimeout(e,t)}),ke=()=>{T=!0,c("SYNC - START"),N(3)},_e=()=>{T=!1,c("SYNC - FAIL"),N(2)},de=()=>{Ge(2e3).then(()=>{T=!1}),c("SYNC - DONE"),N(4)},O=async()=>{if(T)return c("SYNC - ALREADY IN PROGRESS"),!1;ke();let t=await S("SYNC");if(!t)return _e(),!1;let{folderId:e,folderLocation:o,assetsFolderId:n,files:i}=t,r=await k("notes");if(!r)return de(),!1;let a=await ae(r,i,{getFile:$e}),s=await me(e,a,{createFile:Le,updateFile:je}),m=new Date().toISOString();return await Y({notes:s,sync:{folderId:e,folderLocation:o,assetsFolderId:n,lastSync:m},setBy:`sync-${m}`}),de(),!0},M=async t=>{let e=await S("SYNC_DELETE_FILE");if(!e)return!1;let{files:o}=e;return t&&o.find(i=>i.id===t)!==void 0?(c(`%cSYNC_DELETE_FILE - DELETING FILE - ${t}`,"red"),Ae(t)):(c(`SYNC_DELETE_FILE - PROBLEM - cannot delete file with ID ${t}`),!1)};var E=t=>{if(t.type===0){v().then(e=>e&&O());return}if(t.type===1){O();return}if(t.type===6&&t.payload){let e=t.payload;M(e);return}t.type===5&&l()},le=()=>{chrome.runtime.onMessage.addListener(E)};var fe=(t,e)=>!!t[e]?.locked;var pe=t=>`<a href="${t}" target="_blank">${t}</a>`,Ye=t=>{let{pageUrl:e}=t;return`${pe(e)}<br><br>`},Re=t=>{let{srcUrl:e}=t;return`<img src="${e}"><br><br>`},Ue=t=>{let{pageUrl:e,selectionText:o}=t,n=pe(e);return`${o??""}<br><b>(${n})</b><br><br>`},Be={page:Ye,image:Re,selection:Ue},ue=(t,e)=>{let o=Be[t];return o?o(e):""};var ge="@clipboard",Ne="@images",ye="@received";var I=(t,e)=>{chrome.storage.local.get(["notes"],o=>{let n=o.notes,i=new Date().toISOString();n[e]=e in n?{...n[e],content:t+n[e].content,modifiedTime:i}:{content:t,createdTime:i,modifiedTime:i},chrome.storage.local.set({notes:n,setBy:`worker-${i}`,lastEdit:i})})},Te=t=>{chrome.storage.local.get(["id"],e=>{if(!e.id)return;let o={text:t,sender:e.id};chrome.storage.sync.set({selection:o})})},Oe=()=>chrome.runtime.onMessage.addListener(t=>{if(t.type!==7)return;let{targetNoteName:e,data:o}=t.payload;!e||!o||chrome.storage.local.get("notes",n=>{let i=n.notes;if(!(e in i))return;let r=i[e].content,a=`${o}<br><br>${r}`,s=new Date().toISOString();i[e]={...i[e],content:a,modifiedTime:s},chrome.storage.local.set({notes:i,setBy:`worker-${s}`,lastEdit:s})})}),be=()=>{chrome.storage.onChanged.addListener((t,e)=>{if(e==="sync"&&t.selection){let o=t.selection.newValue;if(!o||!o.text)return;chrome.storage.local.get(["id"],n=>{o.sender!==n.id&&I(o.text,ye)})}})};var he="my-notes",ve=["page","image","selection"],He=t=>chrome.contextMenus.create({id:he,title:"My Notes",contexts:ve},()=>ve.forEach(e=>{let o=[ge,e==="image"?Ne:""].filter(Boolean),n=Object.keys(t).filter(s=>!o.includes(s)).sort(),i={parentId:he,contexts:[e]},r=s=>({...i,id:`${e}-note-${s}`,title:f(`Context Menu.${e}-note.title`,{note:s}),enabled:!fe(t,s)}),a=s=>({...i,type:"separator",id:`${e}-separator-${s}`});o.forEach(s=>{chrome.contextMenus.create(r(s))}),chrome.contextMenus.create(a("first")),n.forEach(s=>{chrome.contextMenus.create(r(s))}),chrome.contextMenus.create(a("second")),chrome.contextMenus.create({...i,id:`${e}-remote`,title:f(`Context Menu.${e}-remote.title`)})})),xe=()=>chrome.contextMenus.onClicked.addListener(t=>{let{context:e,destination:o,noteName:n}=y(t.menuItemId.toString()),i=`Context Menu.${e}-${o}.notification`,r=ue(e,t);if(r){if(o==="note"&&n){I(r,n),h({notificationId:`note-${new Date().getTime()}-${n}`,message:f(i,{note:n})});return}o==="remote"&&(Te(r),h({notificationId:`remote-${new Date().getTime()}`,message:f(i)}))}}),D,Se=t=>{if(!t){D="",chrome.contextMenus.removeAll();return}let e=JSON.stringify(Object.keys(t).map(o=>`${o}_${t[o].locked}`));e!==D&&(D=e,chrome.contextMenus.removeAll(()=>{He(t)}))},Ce=()=>{chrome.storage.local.get("notes",t=>{Se(t.notes)}),chrome.storage.onChanged.addListener((t,e)=>{e==="local"&&t.notes&&Se(t.notes.newValue)})};var ze=["identity"],F={identity:t=>E({type:t?0:5})},Me=(t,e,{having:o})=>{let n=e.permissions;n&&Object.keys(t).filter(i=>n.includes(i)).forEach(i=>{c(`Permissions - Acting on ${o?"granted":"removed"} permission "${i}"`),t[i](o)})},Ee=()=>{ze.forEach(t=>{p(t).then(e=>!e&&F[t](e))}),chrome.permissions.onAdded.addListener(t=>Me(F,t,{having:!0})),chrome.permissions.onRemoved.addListener(t=>Me(F,t,{having:!1}))};ee();te();le();xe();Ce();Oe();be();Ee();Z();chrome.runtime.onInstalled.addListener(t=>{V(),q(),Q(t)});

```









</details>

</details>



</details>
                                           

***                              




<details><summary> Pretty Print JS </summary> 

Site:                                   
https://beautifier.io                         

Repo:                         
https://github.com/beautifier/js-beautify



<details><summary> Code [ 648 ish line count ] </summary>                               


  
```
import {
    a as k,
    b as _,
    c as Y,
    f as R,
    g as u,
    h as U,
    i as B,
    j as H,
    k as g,
    l as N,
    m as c,
    n as l,
    o as z
} from "./chunks/chunk-CHQ6UX2I.mjs";
import {
    a as w,
    d as P,
    e as $,
    f as L,
    g as d,
    h as j,
    i as A,
    j as G
} from "./chunks/chunk-Y4ESULC7.mjs";
import {
    c as p
} from "./chunks/chunk-ZZJPW3A4.mjs";
import {
    g as f
} from "./chunks/chunk-KYTTGGZV.mjs";

function Ie() {
    let t = new Uint8Array(32);
    crypto.getRandomValues(t);
    let e = "";
    for (let o = 0; o < t.length; o += 1) e += t[o].toString(16);
    return e
}
var V = () => {
    chrome.storage.local.get(["id"], t => {
        if (t.id) return;
        let e = Ie();
        chrome.storage.local.set({
            id: e
        })
    })
};
var Fe = () => {
        let t = new Date().toISOString(),
            e = t,
            o = t;
        return {
            One: {
                content: "",
                createdTime: e,
                modifiedTime: o
            },
            Two: {
                content: "",
                createdTime: e,
                modifiedTime: o
            },
            Three: {
                content: "",
                createdTime: e,
                modifiedTime: o
            }
        }
    },
    K = t => {
        let e = t ? Fe() : {};
        return {
            font: {
                id: "helvetica",
                name: "Helvetica",
                genericFamily: "sans-serif",
                fontFamily: "Helvetica, sans-serif"
            },
            size: 200,
            theme: "light",
            customTheme: "",
            sidebar: !0,
            toolbar: !0,
            notes: e,
            order: [],
            active: "One",
            setBy: "",
            lastEdit: "",
            notesOrder: "Alphabetical",
            focus: !1,
            tab: !1,
            tabSize: -1,
            autoSync: !1,
            openNoteOnMouseHover: !1
        }
    };
var J = ["font", "size", "theme", "customTheme", "sidebar", "toolbar", "notes", "order", "active", "setBy", "lastEdit", "notesOrder", "focus", "tab", "tabSize", "autoSync", "openNoteOnMouseHover"],
    W = (t, e) => {
        let o = K(!0),
            n = t.value || t.newtab || t.notes || e.notes || o.notes;
        if (typeof n == "string" && (n = [n, "", ""]), Array.isArray(n) && n.length === 3 && n.every(s => typeof s == "string")) {
            let s = new Date().toISOString(),
                m = s,
                b = s;
            n = {
                One: {
                    content: n[0],
                    createdTime: m,
                    modifiedTime: b
                },
                Two: {
                    content: n[1],
                    createdTime: m,
                    modifiedTime: b
                },
                Three: {
                    content: n[2],
                    createdTime: m,
                    modifiedTime: b
                }
            }
        }
        let i = s => s in n ? s : null,
            r = Object.keys(n).sort()[0] || null;
        return {
            font: w(e.font) ? e.font : o.font,
            size: P(e.size) ? e.size : o.size,
            theme: $(e.theme) ? e.theme : o.theme,
            customTheme: L(e.customTheme) ? e.customTheme : o.customTheme,
            sidebar: d(e.sidebar) ? e.sidebar : o.sidebar,
            toolbar: d(e.toolbar) ? e.toolbar : o.toolbar,
            notes: n,
            order: j(e.order) ? e.order : [],
            active: i(e.active) || i(o.active) || r,
            setBy: typeof e.setBy == "string" ? e.setBy : o.setBy,
            lastEdit: typeof e.lastEdit == "string" ? e.lastEdit : o.lastEdit,
            notesOrder: G(e.notesOrder) ? e.notesOrder : "Alphabetical",
            focus: d(e.focus) ? e.focus : o.focus,
            tab: d(e.tab) ? e.tab : o.tab,
            tabSize: A(e.tabSize) ? e.tabSize : o.tabSize,
            autoSync: d(e.autoSync) ? e.autoSync : o.autoSync,
            openNoteOnMouseHover: d(e.openNoteOnMouseHover) ? e.openNoteOnMouseHover : o.openNoteOnMouseHover
        }
    };
var q = () => {
    chrome.storage.sync.get(["newtab", "value", "notes"], t => {
        chrome.storage.local.get(J, e => {
            let o = W(t, e);
            chrome.storage.local.set(o), chrome.storage.sync.remove(["newtab", "value", "notes"])
        })
    })
};
var y = t => {
    let [e, o, ...n] = t.split("-");
    return {
        context: e,
        destination: o,
        noteName: n.join("-")
    }
};
var Q = t => {
        if (t.reason !== "update") return;
        let e = {
            type: 0,
            payload: chrome.runtime.getManifest().version
        };
        chrome.storage.local.set({
            notification: e
        })
    },
    h = ({
        notificationId: t,
        message: e
    }) => chrome.notifications.create(t, {
        type: "basic",
        title: "My Notes",
        message: e,
        iconUrl: "images/icon128.png"
    }),
    Z = () => {
        chrome.notifications.onClicked.addListener(t => {
            let {
                context: e,
                noteName: o
            } = y(t);
            e === "note" && o && chrome.storage.local.get(["notes"], n => {
                o in n.notes && chrome.tabs.create({
                    url: `notes.html?note=${o}`
                })
            })
        })
    };
var X = () => chrome.tabs.create({
        url: "/notes.html"
    }),
    ee = () => chrome.action.onClicked.addListener(X),
    te = () => chrome.commands.onCommand.addListener(t => {
        t === "open-my-notes" && X()
    });
var v = async () => {
    if (!await p("identity")) return;
    let e = await u() || await R();
    if (!e) return;
    let o = `https://drive.google.com/drive/u/0/folders/${e}`,
        n = await B(e) || await U(e),
        i = {
            folderId: e,
            folderLocation: o,
            assetsFolderId: n
        };
    return await _("sync", i), i
};
var S = async t => {
    let e = await z(t);
    if (!e) return;
    let o = await u();
    if (!o || o !== e.folderId) {
        await l();
        return
    }
    if (e.folderLocation !== `https://drive.google.com/drive/u/0/folders/${o}`) {
        c(`${t} - PROBLEM - folderLocation not correct`), await l();
        return
    }
    let n = await H(e.folderId);
    if (!Array.isArray(n)) {
        c(`${t} - PROBLEM - cannot retrieve files`), await l();
        return
    }
    return {
        ...e,
        files: n
    }
};
var we = (t, e) => Object.keys(t).filter(n => {
        let i = t[n],
            r = i.sync?.file.id;
        return i.sync?.file.id && i.sync?.file.modifiedTime === i.modifiedTime && e.find(s => s.id === r) === void 0
    }),
    oe = (t, e) => {
        let o = {
            ...t
        };
        return we(o, e).forEach(n => {
            c(`SYNC - IN - DELETING NOTE - ${n}`, "red"), delete o[n]
        }), o
    };
var Pe = (t, e) => {
        let o = Object.keys(t),
            n = Object.values(t).map(r => r.sync?.file.id);
        return e.filter(r => !o.includes(r.name) && !n.includes(r.id))
    },
    ne = async (t, e, o) => {
        let n = {
                ...t
            },
            i = Pe(n, e);
        for await (let r of i) {
            let a = await o(r.id) || "";
            c(`SYNC - IN - CREATING NOTE - ${r.name}`, "green"), n[r.name] = {
                content: a,
                createdTime: r.createdTime,
                modifiedTime: r.modifiedTime,
                sync: {
                    file: r
                }
            }
        }
        return n
    };
var x = (t, e, o) => ({
        ...t,
        content: e,
        createdTime: o.createdTime,
        modifiedTime: o.modifiedTime,
        sync: {
            file: {
                id: o.id,
                name: o.name,
                createdTime: o.createdTime,
                modifiedTime: o.modifiedTime
            }
        }
    }),
    re = (t, e) => `${t}<br><br>${e}`,
    ie = async (t, e, o, n, i) => {
        let r = {
                ...t
            },
            a = Object.keys(r).find(m => r[m] === e),
            s = await n(o.id) || "";
        return c(`SYNC - IN - UPDATING NOTE - ${o.name} (name before: ${a||o.name}, note MT: ${e.modifiedTime}, file MT: ${o.modifiedTime})`, "blue"), r[o.name] = x(e, i === "replace" ? s : re(e.content, s), o), a && a !== o.name && delete r[a], r
    }, se = async (t, e, o) => {
        let n = {
            ...t
        };
        for await (let i of e) {
            let r = Object.values(t).find(a => a.sync?.file.id === i.id);
            if (r && r.sync && r.modifiedTime === r.sync.file.modifiedTime && i.modifiedTime > r.modifiedTime && (n = await ie(n, r, i, o, "replace")), r && r.sync && r.modifiedTime !== r.sync.file.modifiedTime && i.modifiedTime > r.modifiedTime && (n = await ie(n, r, i, o, "merge")), !r && i.name in n && n[i.name].modifiedTime === i.modifiedTime && (c(`SYNC - IN - CONNECTING NOTE - ${i.name} (note MT: ${n[i.name].modifiedTime}, file MT: ${i.modifiedTime})`, "blue"), n[i.name] = x(n[i.name], n[i.name].content, i)), !r && i.name in n && n[i.name].modifiedTime !== i.modifiedTime) {
                let a = await o(i.id) || "";
                c(`SYNC - IN - UPDATING NOTE - ${i.name} (note MT: ${n[i.name].modifiedTime}, file MT: ${i.modifiedTime})`, "blue"), n[i.name] = x(n[i.name], re(n[i.name].content, a), i)
            }
        }
        return n
    };
var ae = async (t, e, {
    getFile: o
}) => {
    let n = oe(t, e),
        i = await ne(n, e, o);
    return await se(i, e, o)
};
var ce = (t, e) => ({
        id: e.id,
        name: e.name,
        createdTime: e.createdTime || t.createdTime,
        modifiedTime: e.modifiedTime
    }),
    me = async (t, e, {
        createFile: o,
        updateFile: n
    }) => {
        let i = {
            ...e
        };
        for await (let r of Object.keys(i)) {
            let a = i[r];
            if (!a.sync) {
                c(`SYNC - OUT - CREATING FILE - ${r}`);
                let s = await o(t, {
                    ...a,
                    name: r
                });
                a.sync = {
                    file: ce(a, s)
                };
                continue
            }
            if (a.modifiedTime > a.sync.file.modifiedTime) {
                c(`SYNC - OUT - UPDATING FILE - ${r} (name before: ${a.sync.file.name})`);
                let s = await n(a.sync.file.id, {
                    ...a,
                    name: r
                });
                a.sync = {
                    file: ce(a, s)
                }
            }
        }
        return i
    };
var {
    getFile: $e,
    createFile: Le,
    updateFile: je,
    deleteFile: Ae
} = g, T = !1, Ge = t => new Promise(e => {
    setTimeout(e, t)
}), ke = () => {
    T = !0, c("SYNC - START"), N(3)
}, _e = () => {
    T = !1, c("SYNC - FAIL"), N(2)
}, de = () => {
    Ge(2e3).then(() => {
        T = !1
    }), c("SYNC - DONE"), N(4)
}, O = async () => {
    if (T) return c("SYNC - ALREADY IN PROGRESS"), !1;
    ke();
    let t = await S("SYNC");
    if (!t) return _e(), !1;
    let {
        folderId: e,
        folderLocation: o,
        assetsFolderId: n,
        files: i
    } = t, r = await k("notes");
    if (!r) return de(), !1;
    let a = await ae(r, i, {
            getFile: $e
        }),
        s = await me(e, a, {
            createFile: Le,
            updateFile: je
        }),
        m = new Date().toISOString();
    return await Y({
        notes: s,
        sync: {
            folderId: e,
            folderLocation: o,
            assetsFolderId: n,
            lastSync: m
        },
        setBy: `sync-${m}`
    }), de(), !0
}, M = async t => {
    let e = await S("SYNC_DELETE_FILE");
    if (!e) return !1;
    let {
        files: o
    } = e;
    return t && o.find(i => i.id === t) !== void 0 ? (c(`%cSYNC_DELETE_FILE - DELETING FILE - ${t}`, "red"), Ae(t)) : (c(`SYNC_DELETE_FILE - PROBLEM - cannot delete file with ID ${t}`), !1)
};
var E = t => {
        if (t.type === 0) {
            v().then(e => e && O());
            return
        }
        if (t.type === 1) {
            O();
            return
        }
        if (t.type === 6 && t.payload) {
            let e = t.payload;
            M(e);
            return
        }
        t.type === 5 && l()
    },
    le = () => {
        chrome.runtime.onMessage.addListener(E)
    };
var fe = (t, e) => !!t[e]?.locked;
var pe = t => `<a href="${t}" target="_blank">${t}</a>`,
    Ye = t => {
        let {
            pageUrl: e
        } = t;
        return `${pe(e)}<br><br>`
    },
    Re = t => {
        let {
            srcUrl: e
        } = t;
        return `<img src="${e}"><br><br>`
    },
    Ue = t => {
        let {
            pageUrl: e,
            selectionText: o
        } = t, n = pe(e);
        return `${o??""}<br><b>(${n})</b><br><br>`
    },
    Be = {
        page: Ye,
        image: Re,
        selection: Ue
    },
    ue = (t, e) => {
        let o = Be[t];
        return o ? o(e) : ""
    };
var ge = "@clipboard",
    Ne = "@images",
    ye = "@received";
var I = (t, e) => {
        chrome.storage.local.get(["notes"], o => {
            let n = o.notes,
                i = new Date().toISOString();
            n[e] = e in n ? {
                ...n[e],
                content: t + n[e].content,
                modifiedTime: i
            } : {
                content: t,
                createdTime: i,
                modifiedTime: i
            }, chrome.storage.local.set({
                notes: n,
                setBy: `worker-${i}`,
                lastEdit: i
            })
        })
    },
    Te = t => {
        chrome.storage.local.get(["id"], e => {
            if (!e.id) return;
            let o = {
                text: t,
                sender: e.id
            };
            chrome.storage.sync.set({
                selection: o
            })
        })
    },
    Oe = () => chrome.runtime.onMessage.addListener(t => {
        if (t.type !== 7) return;
        let {
            targetNoteName: e,
            data: o
        } = t.payload;
        !e || !o || chrome.storage.local.get("notes", n => {
            let i = n.notes;
            if (!(e in i)) return;
            let r = i[e].content,
                a = `${o}<br><br>${r}`,
                s = new Date().toISOString();
            i[e] = {
                ...i[e],
                content: a,
                modifiedTime: s
            }, chrome.storage.local.set({
                notes: i,
                setBy: `worker-${s}`,
                lastEdit: s
            })
        })
    }),
    be = () => {
        chrome.storage.onChanged.addListener((t, e) => {
            if (e === "sync" && t.selection) {
                let o = t.selection.newValue;
                if (!o || !o.text) return;
                chrome.storage.local.get(["id"], n => {
                    o.sender !== n.id && I(o.text, ye)
                })
            }
        })
    };
var he = "my-notes",
    ve = ["page", "image", "selection"],
    He = t => chrome.contextMenus.create({
        id: he,
        title: "My Notes",
        contexts: ve
    }, () => ve.forEach(e => {
        let o = [ge, e === "image" ? Ne : ""].filter(Boolean),
            n = Object.keys(t).filter(s => !o.includes(s)).sort(),
            i = {
                parentId: he,
                contexts: [e]
            },
            r = s => ({
                ...i,
                id: `${e}-note-${s}`,
                title: f(`Context Menu.${e}-note.title`, {
                    note: s
                }),
                enabled: !fe(t, s)
            }),
            a = s => ({
                ...i,
                type: "separator",
                id: `${e}-separator-${s}`
            });
        o.forEach(s => {
            chrome.contextMenus.create(r(s))
        }), chrome.contextMenus.create(a("first")), n.forEach(s => {
            chrome.contextMenus.create(r(s))
        }), chrome.contextMenus.create(a("second")), chrome.contextMenus.create({
            ...i,
            id: `${e}-remote`,
            title: f(`Context Menu.${e}-remote.title`)
        })
    })),
    xe = () => chrome.contextMenus.onClicked.addListener(t => {
        let {
            context: e,
            destination: o,
            noteName: n
        } = y(t.menuItemId.toString()), i = `Context Menu.${e}-${o}.notification`, r = ue(e, t);
        if (r) {
            if (o === "note" && n) {
                I(r, n), h({
                    notificationId: `note-${new Date().getTime()}-${n}`,
                    message: f(i, {
                        note: n
                    })
                });
                return
            }
            o === "remote" && (Te(r), h({
                notificationId: `remote-${new Date().getTime()}`,
                message: f(i)
            }))
        }
    }),
    D, Se = t => {
        if (!t) {
            D = "", chrome.contextMenus.removeAll();
            return
        }
        let e = JSON.stringify(Object.keys(t).map(o => `${o}_${t[o].locked}`));
        e !== D && (D = e, chrome.contextMenus.removeAll(() => {
            He(t)
        }))
    },
    Ce = () => {
        chrome.storage.local.get("notes", t => {
            Se(t.notes)
        }), chrome.storage.onChanged.addListener((t, e) => {
            e === "local" && t.notes && Se(t.notes.newValue)
        })
    };
var ze = ["identity"],
    F = {
        identity: t => E({
            type: t ? 0 : 5
        })
    },
    Me = (t, e, {
        having: o
    }) => {
        let n = e.permissions;
        n && Object.keys(t).filter(i => n.includes(i)).forEach(i => {
            c(`Permissions - Acting on ${o?"granted":"removed"} permission "${i}"`), t[i](o)
        })
    },
    Ee = () => {
        ze.forEach(t => {
            p(t).then(e => !e && F[t](e))
        }), chrome.permissions.onAdded.addListener(t => Me(F, t, {
            having: !0
        })), chrome.permissions.onRemoved.addListener(t => Me(F, t, {
            having: !1
        }))
    };
ee();
te();
le();
xe();
Ce();
Oe();
be();
Ee();
Z();
chrome.runtime.onInstalled.addListener(t => {
    V(), q(), Q(t)
});
```


</details>




</details>



