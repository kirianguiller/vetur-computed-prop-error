#  Linting error when accessing to component data from computed properties #3295 

https://github.com/vuejs/vetur/issues/3295

<!-- Check those before opening an issue -->

- [X] I have searched through existing issues
- [X] I have read through [docs](https://vuejs.github.io/vetur)
- [X] I have read [FAQ](https://vuejs.github.io/vetur/guide/FAQ.html)
- [X] I have tried restarting VS Code or running `Vetur: Restart VLS`

## Info

- Platform: Linux (ubuntu 20.04)
- Vetur version: v0.35.0
- VS Code version: 1.62.3

## Problem

### Explanation 
Vetur return an error in computed property when accessing to a data (through : this.someData).  I'm using the option API. I tried in 2 projects and I have the same error.

### Vue Language Server error : 
```
[Trace - 7:11:26 PM] Sending request 'textDocument/codeAction - (60)'.
Params: {
    "textDocument": {
        "uri": "file:///home/wran/Projects/arborator/ttoo_delete/src/pages/Index.vue"
    },
    "range": {
        "start": {
            "line": 49,
            "character": 18
        },
        "end": {
            "line": 49,
            "character": 23
        }
    },
    "context": {
        "diagnostics": [
            {
                "range": {
                    "start": {
                        "line": 49,
                        "character": 18
                    },
                    "end": {
                        "line": 49,
                        "character": 23
                    }
                },
                "message": "Property 'todos' does not exist on type 'CreateComponentPublicInstance<{ [x: string & `on${string}`]: ((...args: any[]) => any) | undefined; } | { [x: string & `on${string}`]: undefined; }, {}, {}, {}, {}, ComponentOptionsMixin, ComponentOptionsMixin, ... 10 more ..., {}>'.\n  Property 'todos' does not exist on type '{ $: ComponentInternalInstance; $data: {}; $props: { [x: string & `on${string}`]: ((...args: any[]) => any) | undefined; } | { [x: string & `on${string}`]: undefined; }; ... 10 more ...; $watch(source: string | Function, cb: Function, options?: WatchOptions<...> | undefined): WatchStopHandle; } & ... 4 more ... & Co...'.",
                "code": 2339,
                "severity": 1,
                "source": "Vetur"
            }
        ],
        "only": [
            "quickfix"
        ]
    }
}
```

#### Screenshot 
![Screenshot from 2022-01-02 19-09-13](https://user-images.githubusercontent.com/35531073/147885197-ace91762-b165-4118-8e90-7be0b0402cf3.png)

## Reproducible Case

### Procedure


- Create a new app with quasar (typescript, eslint)
- Open vscode
- Add the following line in `src/pages/Index.vue` :
```typescript
  computed: {
    test() {
      return this.todos
    }
  }
```

You will then see a vetur linting error that : 
```
Property 'todos' does not exist on type 'CreateComponentPublicInstance<{ [x: string & `on${string}`]: ((...args: any[]) => any) | undefined; } | { [x: string & `on${string}`]: undefined; }, {}, {}, {}, {}, ComponentOptionsMixin, ComponentOptionsMixin, ... 10 more ..., {}>'.
  Property 'todos' does not exist on type '{ $: ComponentInternalInstance; $data: {}; $props: { [x: string & `on${string}`]: ((...args: any[]) => any) | undefined; } | { [x: string & `on${string}`]: undefined; }; ... 10 more ...; $watch(source: string | Function, cb: Function, options?: WatchOptions<...> | undefined): WatchStopHandle; } & ... 4 more ... & Co...'.Vetur(2339)
```

### Repo
You can find a full repo of the reproducible problem here : https://github.com/kirianguiller/vetur-computed-prop-error.
You just need to 
```
git clone https://github.com/kirianguiller/vetur-computed-prop-error
cd vetur-computed-prop-error
npm install
```

Then to open vscode and see the error in `src/pages/Index.vue` line 50

## Related Issues 
I've looked at some issues, but I couldn't fix my problem with their recommendations. Here are the similar issues that I found (some of them are linking to other issues too) : 
- https://github.com/vuejs/vetur/issues/2394
- https://github.com/vuejs/vue/issues/9873

Thank you a lot for your help and for your amazing work on making vue + TS so nice :)
