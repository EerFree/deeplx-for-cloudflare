Deploy DeepLX on Cloudflare.

## Usage

Development
```
npm i && npm run dev
```

Deploy
```
npm run deploy
```

Alternatively to deploy, open the [Cloudflare dashboard](https://dash.cloudflare.com/), select `Workds & pages` -> `Create Application` -> `Create Worker` -> `Deploy` -> `Edit Code`, and paste the following code, then click `Save and Deploy`.

```js
var gt=t=>{let r=t.split("/");return r[0]===""&&r.shift(),r},yt=t=>{let r=[];for(let e=0;;){let s=!1;if(t=t.replace(/\{[^}]+\}/g,i=>{let o=`@\\${e}`;return r[e]=[o,i],e++,s=!0,o}),!s)break}let n=t.split("/");n[0]===""&&n.shift();for(let e=r.length-1;e>=0;e--){let[s]=r[e];for(let i=n.length-1;i>=0;i--)if(n[i].indexOf(s)!==-1){n[i]=n[i].replace(s,r[e][1]);break}}return n},z={},rt=t=>{if(t==="*")return"*";let r=t.match(/^\:([^\{\}]+)(?:\{(.+)\})?$/);return r?(z[t]||(r[2]?z[t]=[t,r[1],new RegExp("^"+r[2]+"$")]:z[t]=[t,r[1],!0]),z[t]):null},nt=t=>{let r=t.url.match(/^https?:\/\/[^/]+(\/[^?]*)/);return r?r[1]:""},vt=t=>{let r=t.indexOf("?",8);return r===-1?"":"?"+t.slice(r+1)},wt=t=>{let r=nt(t);return r.length>1&&r[r.length-1]==="/"?r.slice(0,-1):r},I=(...t)=>{let r="",n=!1;for(let e of t)r[r.length-1]==="/"&&(r=r.slice(0,-1),n=!0),e[0]!=="/"&&(e=`/${e}`),e==="/"&&n?r=`${r}/`:e!=="/"&&(r=`${r}${e}`),e==="/"&&r===""&&(r="/");return r},K=t=>{let r=t.match(/^(.+|)(\/\:[^\/]+)\?$/);if(!r)return null;let n=r[1],e=n+r[2];return[n===""?"/":n.replace(/\/$/,""),e]},et=t=>/[%+]/.test(t)?(t.indexOf("+")!==-1&&(t=t.replace(/\+/g," ")),/%/.test(t)?F(t):t):t,_t=(t,r,n)=>{let e;if(!n&&r&&!/[%+]/.test(r)){let o=t.indexOf(`?${r}`,8);for(o===-1&&(o=t.indexOf(`&${r}`,8));o!==-1;){let a=t.charCodeAt(o+r.length+1);if(a===61){let h=o+r.length+2,c=t.indexOf("&",h);return et(t.slice(h,c===-1?void 0:c))}else if(a==38||isNaN(a))return"";o=t.indexOf(`&${r}`,o+1)}if(e=/[%+]/.test(t),!e)return}let s={};e??(e=/[%+]/.test(t));let i=t.indexOf("?",8);for(;i!==-1;){let o=t.indexOf("&",i+1),a=t.indexOf("=",i);a>o&&o!==-1&&(a=-1);let h=t.slice(i+1,a===-1?o===-1?void 0:o:a);if(e&&(h=et(h)),i=o,h==="")continue;let c;a===-1?c="":(c=t.slice(a+1,o===-1?void 0:o),e&&(c=et(c))),n?(s[h]??(s[h]=[])).push(c):s[h]??(s[h]=c)}return r?s[r]:s},xt=_t,Et=(t,r)=>_t(t,r,!0),F=decodeURIComponent;var qt=/^[\w!#$%&'*.^`|~+-]+$/,Bt=/^[ !#-:<-[\]-~]*$/,bt=(t,r)=>t.trim().split(";").reduce((e,s)=>{s=s.trim();let i=s.indexOf("=");if(i===-1)return e;let o=s.substring(0,i).trim();if(r&&r!==o||!qt.test(o))return e;let a=s.substring(i+1).trim();return a.startsWith('"')&&a.endsWith('"')&&(a=a.slice(1,-1)),Bt.test(a)&&(e[o]=F(a)),e},{});var Ut=(t,r,n={})=>{let e=`${t}=${r}`;return n&&typeof n.maxAge=="number"&&n.maxAge>=0&&(e+=`; Max-Age=${Math.floor(n.maxAge)}`),n.domain&&(e+=`; Domain=${n.domain}`),n.path&&(e+=`; Path=${n.path}`),n.expires&&(e+=`; Expires=${n.expires.toUTCString()}`),n.httpOnly&&(e+="; HttpOnly"),n.secure&&(e+="; Secure"),n.sameSite&&(e+=`; SameSite=${n.sameSite}`),n.partitioned&&(e+="; Partitioned"),e},Rt=(t,r,n={})=>(r=encodeURIComponent(r),Ut(t,r,n));var Pt=class{constructor(t){this.writable=t,this.writer=t.getWriter(),this.encoder=new TextEncoder}async write(t){try{typeof t=="string"&&(t=this.encoder.encode(t)),await this.writer.write(t)}catch{}return this}async writeln(t){return await this.write(t+`
`),this}sleep(t){return new Promise(r=>setTimeout(r,t))}async close(){try{await this.writer.close()}catch{}}async pipe(t){this.writer.releaseLock(),await t.pipeTo(this.writable,{preventClose:!0}),this.writer=this.writable.getWriter()}};var Ht="text/plain; charset=UTF-8",C=class{constructor(t,r){this.env={},this._var={},this.finalized=!1,this.error=void 0,this._status=200,this._h=void 0,this._pH=void 0,this._init=!0,this._renderer=n=>this.html(n),this.notFoundHandler=()=>new Response,this.render=(...n)=>this._renderer(...n),this.setRenderer=n=>{this._renderer=n},this.header=(n,e,s)=>{if(e===void 0){this._h?this._h.delete(n):this._pH&&delete this._pH[n.toLocaleLowerCase()],this.finalized&&this.res.headers.delete(n);return}s?.append?(this._h||(this._init=!1,this._h=new Headers(this._pH),this._pH={}),this._h.append(n,e)):this._h?this._h.set(n,e):(this._pH??(this._pH={}),this._pH[n.toLowerCase()]=e),this.finalized&&(s?.append?this.res.headers.append(n,e):this.res.headers.set(n,e))},this.status=n=>{this._status=n},this.set=(n,e)=>{this._var??(this._var={}),this._var[n]=e},this.get=n=>this._var?this._var[n]:void 0,this.newResponse=(n,e,s)=>{if(this._init&&!s&&!e&&this._status===200)return new Response(n,{headers:this._pH});if(e&&typeof e!="number"){let o=new Response(n,e),a=this._pH?.["content-type"];return a&&o.headers.set("content-type",a),o}let i=e??this._status;this._pH??(this._pH={}),this._h??(this._h=new Headers);for(let[o,a]of Object.entries(this._pH))this._h.set(o,a);if(this._res){this._res.headers.forEach((o,a)=>{this._h?.set(a,o)});for(let[o,a]of Object.entries(this._pH))this._h.set(o,a)}s??(s={});for(let[o,a]of Object.entries(s))if(typeof a=="string")this._h.set(o,a);else{this._h.delete(o);for(let h of a)this._h.append(o,h)}return new Response(n,{status:i,headers:this._h})},this.body=(n,e,s)=>typeof e=="number"?this.newResponse(n,e,s):this.newResponse(n,e),this.text=(n,e,s)=>{if(!this._pH){if(this._init&&!s&&!e)return new Response(n);this._pH={}}return this._pH["content-type"]&&(this._pH["content-type"]=Ht),typeof e=="number"?this.newResponse(n,e,s):this.newResponse(n,e)},this.json=(n,e,s)=>{let i=JSON.stringify(n);return this._pH??(this._pH={}),this._pH["content-type"]="application/json; charset=UTF-8",typeof e=="number"?this.newResponse(i,e,s):this.newResponse(i,e)},this.jsonT=(n,e,s)=>{let i=typeof e=="number"?this.json(n,e,s):this.json(n,e);return{response:i,data:n,format:"json",status:i.status}},this.html=(n,e,s)=>(this._pH??(this._pH={}),this._pH["content-type"]="text/html; charset=UTF-8",typeof n=="object"&&(n instanceof Promise||(n=n.toString()),n instanceof Promise)?n.then(i=>typeof e=="number"?this.newResponse(i,e,s):this.newResponse(i,e)):typeof e=="number"?this.newResponse(n,e,s):this.newResponse(n,e)),this.redirect=(n,e=302)=>(this._h??(this._h=new Headers),this._h.set("Location",n),this.newResponse(null,e)),this.streamText=(n,e,s)=>(s??(s={}),this.header("content-type",Ht),this.header("x-content-type-options","nosniff"),this.header("transfer-encoding","chunked"),this.stream(n,e,s)),this.stream=(n,e,s)=>{let{readable:i,writable:o}=new TransformStream,a=new Pt(o);return n(a).finally(()=>a.close()),typeof e=="number"?this.newResponse(i,e,s):this.newResponse(i,e)},this.cookie=(n,e,s)=>{let i=Rt(n,e,s);this.header("set-cookie",i,{append:!0})},this.notFound=()=>this.notFoundHandler(this),this.req=t,r&&(this._exCtx=r.executionCtx,this.env=r.env,r.notFoundHandler&&(this.notFoundHandler=r.notFoundHandler))}get event(){if(this._exCtx&&"respondWith"in this._exCtx)return this._exCtx;throw Error("This context has no FetchEvent")}get executionCtx(){if(this._exCtx)return this._exCtx;throw Error("This context has no ExecutionContext")}get res(){return this._init=!1,this._res||(this._res=new Response("404 Not Found",{status:404}))}set res(t){this._init=!1,this._res&&t&&(this._res.headers.delete("content-type"),this._res.headers.forEach((r,n)=>{t.headers.set(n,r)})),this._res=t,this.finalized=!0}get var(){return{...this._var}}get runtime(){let t=globalThis;return t?.Deno!==void 0?"deno":t?.Bun!==void 0?"bun":typeof t?.WebSocketPair=="function"?"workerd":typeof t?.EdgeRuntime=="string"?"edge-light":t?.fastly!==void 0?"fastly":t?.__lagon__!==void 0?"lagon":t?.process?.release?.name==="node"?"node":"other"}};var st=(t,r,n)=>(e,s)=>{let i=-1;return o(0);function o(a){if(a<=i)throw new Error("next() called multiple times");i=a;let h,c=!1,d;if(t[a]?(d=t[a][0],e instanceof C&&e.req.setParams(t[a][1])):d=a===t.length&&s||void 0,!d)e instanceof C&&e.finalized===!1&&n&&(h=n(e));else try{h=d(e,()=>{let p=o(a+1);return p instanceof Promise?p:Promise.resolve(p)})}catch(p){if(p instanceof Error&&e instanceof C&&r)e.error=p,h=r(p,e),c=!0;else throw p}return h instanceof Promise?h.then(p=>(p!==void 0&&"response"in p&&(p=p.response),p&&e.finalized===!1&&(e.res=p),e)).catch(async p=>{if(p instanceof Error&&e instanceof C&&r)return e.error=p,e.res=await r(p,e),e;throw p}):(h!==void 0&&"response"in h&&(h=h.response),h&&(e.finalized===!1||c)&&(e.res=h),e)}};var Ot=class extends Error{constructor(t=500,r){super(r?.message),this.res=r?.res,this.status=t}getResponse(){return this.res?this.res:new Response(this.message,{status:this.status})}};var Wt=t=>Array.isArray(t),St=async(t,r={all:!1})=>{let n={},e=t.headers.get("Content-Type");if(e&&(e.startsWith("multipart/form-data")||e.startsWith("application/x-www-form-urlencoded"))){let s=await t.formData();if(s){let i={};s.forEach((o,a)=>{if(!(r.all||a.slice(-2)==="[]")){i[a]=o;return}if(i[a]&&Wt(i[a])){i[a].push(o);return}if(i[a]){i[a]=[i[a],o];return}i[a]=o}),n=i}}return n};var Tt=class{constructor(t,r="/",n=[]){this._p={},this.bodyCache={},this.cachedBody=e=>{let{bodyCache:s,raw:i}=this,o=s[e];return o||(s.arrayBuffer?(async()=>await new Response(s.arrayBuffer)[e]())():s[e]=i[e]())},this.raw=t,this.path=r,this._s=n,this.vData={}}setParams(t){this._p=t}param(t){if(this._s)if(t){let r=this._s[this._p[t]]??this._p[t];return r?/\%/.test(r)?F(r):r:void 0}else{let r={},n=Object.keys(this._p);for(let e=0,s=n.length;e<s;e++){let i=n[e],o=this._s[this._p[i]]??this._p[i];o&&typeof o=="string"&&(r[i]=/\%/.test(o)?F(o):o)}return r}return null}query(t){return xt(this.url,t)}queries(t){return Et(this.url,t)}header(t){if(t)return this.raw.headers.get(t.toLowerCase())??void 0;let r={};return this.raw.headers.forEach((n,e)=>{r[e]=n}),r}cookie(t){let r=this.raw.headers.get("Cookie");if(!r)return;let n=bt(r);return t?n[t]:n}async parseBody(t){if(this.bodyCache.parsedBody)return this.bodyCache.parsedBody;let r=await St(this,t);return this.bodyCache.parsedBody=r,r}json(){return this.cachedBody("json")}text(){return this.cachedBody("text")}arrayBuffer(){return this.cachedBody("arrayBuffer")}blob(){return this.cachedBody("blob")}formData(){return this.cachedBody("formData")}addValidatedData(t,r){this.vData[t]=r}valid(t){return this.vData[t]}get url(){return this.raw.url}get method(){return this.raw.method}get headers(){return this.raw.headers}get body(){return this.raw.body}get bodyUsed(){return this.raw.bodyUsed}get integrity(){return this.raw.integrity}get keepalive(){return this.raw.keepalive}get referrer(){return this.raw.referrer}get signal(){return this.raw.signal}};var x="ALL",Lt="all",Q=["get","post","put","delete","options","patch"],V=class extends Error{};function Gt(){return class{}}var zt=t=>t.text("404 Not Found",404),At=(t,r)=>{if(t instanceof Ot)return t.getResponse();console.error(t);let n="Internal Server Error";return r.text(n,500)},it=class extends Gt(){constructor(t={}){super(),this._basePath="/",this.path="/",this.routes=[],this.notFoundHandler=zt,this.errorHandler=At,this.head=()=>(console.warn("`app.head()` is no longer used. `app.get()` implicitly handles the HEAD method."),this),this.handleEvent=e=>this.dispatch(e.request,e,void 0,e.request.method),this.fetch=(e,s,i)=>this.dispatch(e,i,s,e.method),this.request=(e,s,i,o)=>{if(e instanceof Request)return s!==void 0&&(e=new Request(e,s)),this.fetch(e,i,o);e=e.toString();let a=/^https?:\/\//.test(e)?e:`http://localhost${I("/",e)}`,h=new Request(a,s);return this.fetch(h,i,o)},this.fire=()=>{addEventListener("fetch",e=>{e.respondWith(this.dispatch(e.request,e,void 0,e.request.method))})},[...Q,Lt].map(e=>{this[e]=(s,...i)=>(typeof s=="string"?this.path=s:this.addRoute(e,this.path,s),i.map(o=>{typeof o!="string"&&this.addRoute(e,this.path,o)}),this)}),this.on=(e,s,...i)=>{if(!e)return this;this.path=s;for(let o of[e].flat())i.map(a=>{this.addRoute(o.toUpperCase(),this.path,a)});return this},this.use=(e,...s)=>(typeof e=="string"?this.path=e:s.unshift(e),s.map(i=>{this.addRoute(x,this.path,i)}),this);let n=t.strict??!0;delete t.strict,Object.assign(this,t),this.getPath=n?t.getPath??nt:wt}clone(){let t=new it({router:this.router,getPath:this.getPath});return t.routes=this.routes,t}route(t,r){let n=this.basePath(t);return r?(r.routes.map(e=>{let s=r.errorHandler===At?e.handler:async(i,o)=>(await st([],r.errorHandler)(i,()=>e.handler(i,o))).res;n.addRoute(e.method,e.path,s)}),this):n}basePath(t){let r=this.clone();return r._basePath=I(this._basePath,t),r}onError(t){return this.errorHandler=t,this}notFound(t){return this.notFoundHandler=t,this}showRoutes(){this.routes.map(r=>{console.log(`\x1B[32m${r.method}\x1B[0m ${" ".repeat(8-r.method.length)} ${r.path}`)})}mount(t,r,n){let e=I(this._basePath,t),s=e==="/"?0:e.length,i=async(o,a)=>{let h;try{h=o.executionCtx}catch{}let c=n?n(o):[o.env,h],d=Array.isArray(c)?c:[c],p=vt(o.req.url),v=await r(new Request(new URL((o.req.path.slice(s)||"/")+p,o.req.url),o.req.raw),...d);if(v)return v;await a()};return this.addRoute(x,I(t,"*"),i),this}get routerName(){return this.matchRoute("GET","/"),this.router.name}addRoute(t,r,n){t=t.toUpperCase(),r=I(this._basePath,r),this.router.add(t,r,n);let e={path:r,method:t,handler:n};this.routes.push(e)}matchRoute(t,r){return this.router.match(t,r)}handleError(t,r){if(t instanceof Error)return this.errorHandler(t,r);throw t}dispatch(t,r,n,e){if(e==="HEAD")return(async()=>new Response(null,await this.dispatch(t,r,n,"GET")))();let s=this.getPath(t,{env:n}),[i,o]=this.matchRoute(e,s),a=new C(new Tt(t,s,o||[]),{env:n,executionCtx:r,notFoundHandler:this.notFoundHandler});if(i.length===1){let c;a.req.setParams(i[0][1]);try{if(c=i[0][0](a,async()=>{}),!c)return this.notFoundHandler(a)}catch(d){return this.handleError(d,a)}return c instanceof Response||("response"in c&&(c=c.response),c instanceof Response)?c:(async()=>{let d;try{if(d=await c,d!==void 0&&"response"in d&&(d=d.response),!d)return this.notFoundHandler(a)}catch(p){return this.handleError(p,a)}return d})()}let h=st(i,this.errorHandler,this.notFoundHandler);return(async()=>{try{let c=h(a),d=c.constructor.name==="Promise"?await c:c;if(!d.finalized)throw new Error("Context is not finalized. You may forget returning Response object or `await next()`");return d.res}catch(c){return this.handleError(c,a)}})()}};var X="[^/]+",W=".*",G="(?:|/.*)",D=Symbol();function Kt(t,r){return t.length===1?r.length===1?t<r?-1:1:-1:r.length===1||t===W||t===G?1:r===W||r===G?-1:t===X?1:r===X?-1:t.length===r.length?t<r?-1:1:r.length-t.length}var Y=class{constructor(){this.children={}}insert(t,r,n,e,s){if(t.length===0){if(this.index!==void 0)throw D;if(s)return;this.index=r;return}let[i,...o]=t,a=i==="*"?o.length===0?["","",W]:["","",X]:i==="/*"?["","",G]:i.match(/^\:([^\{\}]+)(?:\{(.+)\})?$/),h;if(a){let c=a[1],d=a[2]||X;if(c&&a[2]&&(d=d.replace(/^\((?!\?:)(?=[^)]+\)$)/,"(?:"),/\((?!\?:)/.test(d)))throw D;if(h=this.children[d],!h){if(Object.keys(this.children).some(p=>p!==W&&p!==G))throw D;if(s)return;h=this.children[d]=new Y,c!==""&&(h.varIndex=e.varIndex++)}!s&&c!==""&&n.push([c,h.varIndex])}else if(h=this.children[i],!h){if(Object.keys(this.children).some(c=>c.length>1&&c!==W&&c!==G))throw D;if(s)return;h=this.children[i]=new Y}h.insert(o,r,n,e,s)}buildRegExpStr(){let r=Object.keys(this.children).sort(Kt).map(n=>{let e=this.children[n];return(typeof e.varIndex=="number"?`(${n})@${e.varIndex}`:n)+e.buildRegExpStr()});return typeof this.index=="number"&&r.unshift(`#${this.index}`),r.length===0?"":r.length===1?r[0]:"(?:"+r.join("|")+")"}};var jt=class{constructor(){this.context={varIndex:0},this.root=new Y}insert(t,r,n){let e=[],s=[];for(let o=0;;){let a=!1;if(t=t.replace(/\{[^}]+\}/g,h=>{let c=`@\\${o}`;return s[o]=[c,h],o++,a=!0,c}),!a)break}let i=t.match(/(?::[^\/]+)|(?:\/\*$)|./g)||[];for(let o=s.length-1;o>=0;o--){let[a]=s[o];for(let h=i.length-1;h>=0;h--)if(i[h].indexOf(a)!==-1){i[h]=i[h].replace(a,s[o][1]);break}}return this.root.insert(i,r,e,this.context,n),e}buildRegExp(){let t=this.root.buildRegExpStr();if(t==="")return[/^$/,[],[]];let r=0,n=[],e=[];return t=t.replace(/#(\d+)|@(\d+)|\.\*\$/g,(s,i,o)=>typeof i<"u"?(n[++r]=Number(i),"$()"):(typeof o<"u"&&(e[Number(o)]=++r),"")),[new RegExp(`^${t}`),n,e]}};var ot=[x,...Q].map(t=>t.toUpperCase()),$t=[],Qt=[/^$/,[],{}],at={};function kt(t){return at[t]??(at[t]=new RegExp(t==="*"?"":`^${t.replace(/\/\*/,"(?:|/.*)")}$`))}function Vt(){at={}}function Xt(t){let r=new jt,n=[];if(t.length===0)return Qt;let e=t.map(c=>[!/\*|\/:/.test(c[0]),...c]).sort(([c,d],[p,v])=>c?1:p?-1:d.length-v.length),s={};for(let c=0,d=-1,p=e.length;c<p;c++){let[v,b,T]=e[c];v?s[b]=[T.map(([w])=>[w,{}]),$t]:d++;let _;try{_=r.insert(b,d,v)}catch(w){throw w===D?new V(b):w}v||(n[d]=T.map(([w,O])=>{let A={};for(O-=1;O>=0;O--){let[S,j]=_[O];A[S]=j}return[w,A]}))}let[i,o,a]=r.buildRegExp();for(let c=0,d=n.length;c<d;c++)for(let p=0,v=n[c].length;p<v;p++){let b=n[c][p]?.[1];if(!b)continue;let T=Object.keys(b);for(let _=0,w=T.length;_<w;_++)b[T[_]]=a[b[T[_]]]}let h=[];for(let c in o)h[c]=n[o[c]];return[i,h,s]}function q(t,r){if(t){for(let n of Object.keys(t).sort((e,s)=>s.length-e.length))if(kt(n).test(r))return[...t[n]]}}var ht=class{constructor(){this.name="RegExpRouter",this.middleware={[x]:{}},this.routes={[x]:{}}}add(t,r,n){var e;let{middleware:s,routes:i}=this;if(!s||!i)throw new Error("Can not add a route since the matcher is already built.");ot.indexOf(t)===-1&&ot.push(t),s[t]||[s,i].forEach(h=>{h[t]={},Object.keys(h[x]).forEach(c=>{h[t][c]=[...h[x][c]]})}),r==="/*"&&(r="*");let o=(r.match(/\/:/g)||[]).length;if(/\*$/.test(r)){let h=kt(r);t===x?Object.keys(s).forEach(c=>{var d;(d=s[c])[r]||(d[r]=q(s[c],r)||q(s[x],r)||[])}):(e=s[t])[r]||(e[r]=q(s[t],r)||q(s[x],r)||[]),Object.keys(s).forEach(c=>{(t===x||t===c)&&Object.keys(s[c]).forEach(d=>{h.test(d)&&s[c][d].push([n,o])})}),Object.keys(i).forEach(c=>{(t===x||t===c)&&Object.keys(i[c]).forEach(d=>h.test(d)&&i[c][d].push([n,o]))});return}let a=K(r)||[r];for(let h=0,c=a.length;h<c;h++){let d=a[h];Object.keys(i).forEach(p=>{var v;(t===x||t===p)&&((v=i[p])[d]||(v[d]=[...q(s[p],d)||q(s[x],d)||[]]),i[p][d].push([n,a.length===2&&h===0?o-1:o]))})}}match(t,r){Vt();let n=this.buildAllMatchers();return this.match=(e,s)=>{let i=n[e],o=i[2][s];if(o)return o;let a=s.match(i[0]);if(!a)return[[],$t];let h=a.indexOf("",1);return[i[1][h],a]},this.match(t,r)}buildAllMatchers(){let t={};return ot.forEach(r=>{t[r]=this.buildMatcher(r)||t[x]}),this.middleware=this.routes=void 0,t}buildMatcher(t){let r=[],n=t===x;return[this.middleware,this.routes].forEach(e=>{let s=e[t]?Object.keys(e[t]).map(i=>[i,e[t][i]]):[];s.length!==0?(n||(n=!0),r.push(...s)):t!==x&&r.push(...Object.keys(e[x]).map(i=>[i,e[x][i]]))}),n?Xt(r):null}};var ct=class{constructor(t){this.name="SmartRouter",this.routers=[],this.routes=[],Object.assign(this,t)}add(t,r,n){if(!this.routes)throw new Error("Can not add a route since the matcher is already built.");this.routes.push([t,r,n])}match(t,r){if(!this.routes)throw new Error("Fatal error");let{routers:n,routes:e}=this,s=n.length,i=0,o;for(;i<s;i++){let a=n[i];try{e.forEach(h=>{a.add(...h)}),o=a.match(t,r)}catch(h){if(h instanceof V)continue;throw h}this.match=a.match.bind(a),this.routers=[a],this.routes=void 0;break}if(i===s)throw new Error("Fatal error");return this.name=`SmartRouter + ${this.activeRouter.name}`,o}get activeRouter(){if(this.routes||this.routers.length!==1)throw new Error("No active router has been determined yet.");return this.routers[0]}};var ut=class{constructor(t,r,n){if(this.order=0,this.params={},this.children=n||{},this.methods=[],this.name="",t&&r){let e={};e[t]={handler:r,params:{},possibleKeys:[],score:0,name:this.name},this.methods=[e]}this.patterns=[]}insert(t,r,n){this.name=`${t} ${r}`,this.order=++this.order;let e=this,s=yt(r),i=[],o=[];for(let c=0,d=s.length;c<d;c++){let p=s[c];if(Object.keys(e.children).includes(p)){o.push(...e.patterns),e=e.children[p];let b=rt(p);b&&i.push(b[1]);continue}e.children[p]=new ut;let v=rt(p);v&&(e.patterns.push(v),o.push(...e.patterns),i.push(v[1])),o.push(...e.patterns),e=e.children[p]}e.methods.length||(e.methods=[]);let a={},h={handler:n,params:{},possibleKeys:i,name:this.name,score:this.order};return a[t]=h,e.methods.push(a),e}gHSets(t,r,n){let e=[];for(let s=0,i=t.methods.length;s<i;s++){let o=t.methods[s],a=o[r]||o[x];a!==void 0&&(a.possibleKeys.map(h=>{a.params[h]=n[h]}),e.push(a))}return e}search(t,r){let n=[],e={};this.params={};let i=[this],o=gt(r);for(let h=0,c=o.length;h<c;h++){let d=o[h],p=h===c-1,v=[];for(let b=0,T=i.length;b<T;b++){let _=i[b],w=_.children[d];w&&(p===!0?(w.children["*"]&&n.push(...this.gHSets(w.children["*"],t,{...e,..._.params})),n.push(...this.gHSets(w,t,{...e,..._.params}))):v.push(w));for(let O=0,A=_.patterns.length;O<A;O++){let S=_.patterns[O];if(S==="*"){let $=_.children["*"];$&&(n.push(...this.gHSets($,t,{...e,..._.params})),v.push($));continue}if(d==="")continue;let[j,N,L]=S,R=_.children[j],B=o.slice(h).join("/");if(L instanceof RegExp&&L.test(B)){e[N]=B,n.push(...this.gHSets(R,t,{...e,..._.params}));continue}(L===!0||L instanceof RegExp&&L.test(d))&&typeof j=="string"&&(e[N]=d,p===!0?(n.push(...this.gHSets(R,t,{...e,..._.params})),R.children["*"]&&n.push(...this.gHSets(R.children["*"],t,{...e,..._.params}))):(R.params={...e},v.push(R)))}}i=v}return[n.sort((h,c)=>h.score-c.score).map(({handler:h,params:c})=>[h,c])]}};var lt=class{constructor(){this.name="TrieRouter",this.node=new ut}add(t,r,n){let e=K(r);if(e){for(let s of e)this.node.insert(t,s,n);return}this.node.insert(t,r,n)}match(t,r){return this.node.search(t,r)}};var ft=class extends it{constructor(t={}){super(t),this.router=t.router??new ct({routers:[new ht,new lt]})}};function dt(){dt=function(){return r};var t,r={},n=Object.prototype,e=n.hasOwnProperty,s=Object.defineProperty||function(l,u,f){l[u]=f.value},i=typeof Symbol=="function"?Symbol:{},o=i.iterator||"@@iterator",a=i.asyncIterator||"@@asyncIterator",h=i.toStringTag||"@@toStringTag";function c(l,u,f){return Object.defineProperty(l,u,{value:f,enumerable:!0,configurable:!0,writable:!0}),l[u]}try{c({},"")}catch{c=function(u,f,g){return u[f]=g}}function d(l,u,f,g){var m=u&&u.prototype instanceof O?u:O,y=Object.create(m.prototype),E=new Z(g||[]);return s(y,"_invoke",{value:Ft(l,f,E)}),y}function p(l,u,f){try{return{type:"normal",arg:l.call(u,f)}}catch(g){return{type:"throw",arg:g}}}r.wrap=d;var v="suspendedStart",b="suspendedYield",T="executing",_="completed",w={};function O(){}function A(){}function S(){}var j={};c(j,o,function(){return this});var N=Object.getPrototypeOf,L=N&&N(N(tt([])));L&&L!==n&&e.call(L,o)&&(j=L);var R=S.prototype=O.prototype=Object.create(j);function B(l){["next","throw","return"].forEach(function(u){c(l,u,function(f){return this._invoke(u,f)})})}function $(l,u){function f(m,y,E,P){var H=p(l[m],l,y);if(H.type!=="throw"){var M=H.arg,U=M.value;return U&&typeof U=="object"&&e.call(U,"__await")?u.resolve(U.__await).then(function(k){f("next",k,E,P)},function(k){f("throw",k,E,P)}):u.resolve(U).then(function(k){M.value=k,E(M)},function(k){return f("throw",k,E,P)})}P(H.arg)}var g;s(this,"_invoke",{value:function(m,y){function E(){return new u(function(P,H){f(m,y,P,H)})}return g=g?g.then(E,E):E()}})}function Ft(l,u,f){var g=v;return function(m,y){if(g===T)throw new Error("Generator is already running");if(g===_){if(m==="throw")throw y;return{value:t,done:!0}}for(f.method=m,f.arg=y;;){var E=f.delegate;if(E){var P=mt(E,f);if(P){if(P===w)continue;return P}}if(f.method==="next")f.sent=f._sent=f.arg;else if(f.method==="throw"){if(g===v)throw g=_,f.arg;f.dispatchException(f.arg)}else f.method==="return"&&f.abrupt("return",f.arg);g=T;var H=p(l,u,f);if(H.type==="normal"){if(g=f.done?_:b,H.arg===w)continue;return{value:H.arg,done:f.done}}H.type==="throw"&&(g=_,f.method="throw",f.arg=H.arg)}}}function mt(l,u){var f=u.method,g=l.iterator[f];if(g===t)return u.delegate=null,f==="throw"&&l.iterator.return&&(u.method="return",u.arg=t,mt(l,u),u.method==="throw")||f!=="return"&&(u.method="throw",u.arg=new TypeError("The iterator does not provide a '"+f+"' method")),w;var m=p(g,l.iterator,u.arg);if(m.type==="throw")return u.method="throw",u.arg=m.arg,u.delegate=null,w;var y=m.arg;return y?y.done?(u[l.resultName]=y.value,u.next=l.nextLoc,u.method!=="return"&&(u.method="next",u.arg=t),u.delegate=null,w):y:(u.method="throw",u.arg=new TypeError("iterator result is not an object"),u.delegate=null,w)}function Dt(l){var u={tryLoc:l[0]};1 in l&&(u.catchLoc=l[1]),2 in l&&(u.finallyLoc=l[2],u.afterLoc=l[3]),this.tryEntries.push(u)}function J(l){var u=l.completion||{};u.type="normal",delete u.arg,l.completion=u}function Z(l){this.tryEntries=[{tryLoc:"root"}],l.forEach(Dt,this),this.reset(!0)}function tt(l){if(l||l===""){var u=l[o];if(u)return u.call(l);if(typeof l.next=="function")return l;if(!isNaN(l.length)){var f=-1,g=function m(){for(;++f<l.length;)if(e.call(l,f))return m.value=l[f],m.done=!1,m;return m.value=t,m.done=!0,m};return g.next=g}}throw new TypeError(typeof l+" is not iterable")}return A.prototype=S,s(R,"constructor",{value:S,configurable:!0}),s(S,"constructor",{value:A,configurable:!0}),A.displayName=c(S,h,"GeneratorFunction"),r.isGeneratorFunction=function(l){var u=typeof l=="function"&&l.constructor;return!!u&&(u===A||(u.displayName||u.name)==="GeneratorFunction")},r.mark=function(l){return Object.setPrototypeOf?Object.setPrototypeOf(l,S):(l.__proto__=S,c(l,h,"GeneratorFunction")),l.prototype=Object.create(R),l},r.awrap=function(l){return{__await:l}},B($.prototype),c($.prototype,a,function(){return this}),r.AsyncIterator=$,r.async=function(l,u,f,g,m){m===void 0&&(m=Promise);var y=new $(d(l,u,f,g),m);return r.isGeneratorFunction(u)?y:y.next().then(function(E){return E.done?E.value:y.next()})},B(R),c(R,h,"Generator"),c(R,o,function(){return this}),c(R,"toString",function(){return"[object Generator]"}),r.keys=function(l){var u=Object(l),f=[];for(var g in u)f.push(g);return f.reverse(),function m(){for(;f.length;){var y=f.pop();if(y in u)return m.value=y,m.done=!1,m}return m.done=!0,m}},r.values=tt,Z.prototype={constructor:Z,reset:function(l){if(this.prev=0,this.next=0,this.sent=this._sent=t,this.done=!1,this.delegate=null,this.method="next",this.arg=t,this.tryEntries.forEach(J),!l)for(var u in this)u.charAt(0)==="t"&&e.call(this,u)&&!isNaN(+u.slice(1))&&(this[u]=t)},stop:function(){this.done=!0;var l=this.tryEntries[0].completion;if(l.type==="throw")throw l.arg;return this.rval},dispatchException:function(l){if(this.done)throw l;var u=this;function f(H,M){return y.type="throw",y.arg=l,u.next=H,M&&(u.method="next",u.arg=t),!!M}for(var g=this.tryEntries.length-1;g>=0;--g){var m=this.tryEntries[g],y=m.completion;if(m.tryLoc==="root")return f("end");if(m.tryLoc<=this.prev){var E=e.call(m,"catchLoc"),P=e.call(m,"finallyLoc");if(E&&P){if(this.prev<m.catchLoc)return f(m.catchLoc,!0);if(this.prev<m.finallyLoc)return f(m.finallyLoc)}else if(E){if(this.prev<m.catchLoc)return f(m.catchLoc,!0)}else{if(!P)throw new Error("try statement without catch or finally");if(this.prev<m.finallyLoc)return f(m.finallyLoc)}}}},abrupt:function(l,u){for(var f=this.tryEntries.length-1;f>=0;--f){var g=this.tryEntries[f];if(g.tryLoc<=this.prev&&e.call(g,"finallyLoc")&&this.prev<g.finallyLoc){var m=g;break}}m&&(l==="break"||l==="continue")&&m.tryLoc<=u&&u<=m.finallyLoc&&(m=null);var y=m?m.completion:{};return y.type=l,y.arg=u,m?(this.method="next",this.next=m.finallyLoc,w):this.complete(y)},complete:function(l,u){if(l.type==="throw")throw l.arg;return l.type==="break"||l.type==="continue"?this.next=l.arg:l.type==="return"?(this.rval=this.arg=l.arg,this.method="return",this.next="end"):l.type==="normal"&&u&&(this.next=u),w},finish:function(l){for(var u=this.tryEntries.length-1;u>=0;--u){var f=this.tryEntries[u];if(f.finallyLoc===l)return this.complete(f.completion,f.afterLoc),J(f),w}},catch:function(l){for(var u=this.tryEntries.length-1;u>=0;--u){var f=this.tryEntries[u];if(f.tryLoc===l){var g=f.completion;if(g.type==="throw"){var m=g.arg;J(f)}return m}}throw new Error("illegal catch attempt")},delegateYield:function(l,u,f){return this.delegate={iterator:tt(l),resultName:u,nextLoc:f},this.method==="next"&&(this.arg=t),w}},r}function Ct(t,r,n,e,s,i,o){try{var a=t[i](o),h=a.value}catch(c){n(c);return}a.done?r(h):Promise.resolve(h).then(e,s)}function Yt(t){return function(){var r=this,n=arguments;return new Promise(function(e,s){var i=t.apply(r,n);function o(h){Ct(i,e,s,o,a,"next",h)}function a(h){Ct(i,e,s,o,a,"throw",h)}o(void 0)})}}var Jt="https://www2.deepl.com/jsonrpc",Nt=3;function Zt(t,r){return t===void 0&&(t="auto"),r===void 0&&(r="en"),{jsonrpc:"2.0",method:"LMT_handle_texts",id:Math.floor(Math.random()*1e5+1e5)*1e3,params:{texts:[{text:"",requestAlternatives:Nt}],timestamp:0,splitting:"newlines",lang:{source_lang_user_selected:t,target_lang:r}}}}function te(t){return(t||"").split("i").length-1}function ee(t){var r=new Date().getTime();return t!==0?r-r%(t+1)+(t+1):r}function re(t){var r=Zt(t.source_lang,t.target_lang);r.params.texts=[{text:t.text,requestAlternatives:Nt}],r.params.timestamp=ee(te(t.text));var n=JSON.stringify(r);return[0,3].includes((r.id+5)%29)||(r.id+3)%13===0?n=n.replace('"method":"','"method" : "'):n=n.replace('"method":"','"method": "'),n}function Mt(t,r){return pt.apply(this,arguments)}function pt(){return pt=Yt(dt().mark(function t(r,n){var e,s,i,o,a,h;return dt().wrap(function(d){for(;;)switch(d.prev=d.next){case 0:if(r!=null&&r.text){d.next=2;break}return d.abrupt("return",{code:404,message:"No Translate Text Found",data:null});case 2:return d.next=4,fetch((e=n?.proxyEndpoint)!=null?e:Jt,{headers:{"Content-Type":"application/json; charset=utf-8"},method:"POST",body:re(r)});case 4:if(s=d.sent,!s.ok){d.next=13;break}return d.next=8,s.json();case 8:return a=d.sent,h=a.result,d.abrupt("return",{code:200,message:"success",data:h==null||(i=h.texts)==null||(i=i[0])==null?void 0:i.text,source_lang:r?.source_lang||"auto",target_lang:r?.target_lang||"en",alternatives:(o=h.texts)==null||(o=o[0])==null||(o=o.alternatives)==null||o.map==null?void 0:o.map(function(p){return p.text})});case 13:return d.abrupt("return",{code:s.status,data:null,message:s.status===429?"Too many requests, please try again later.":"Unknown error."});case 14:case"end":return d.stop()}},t)})),pt.apply(this,arguments)}var It=new ft;It.get("/",t=>t.redirect("/translate")).get("/translate",t=>t.text("Please use POST method :)")).post("/translate",async t=>{let r=await t.req.json().catch(()=>({})),n=await Mt(r,{proxyEndpoint:"https://ideepl.vercel.app/jsonrpc"});return t.json(n,n.code)});var Br=It;export{Br as default};
```
