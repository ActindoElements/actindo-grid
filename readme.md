## &lt;actindo-grid&gt;

`<actindo-grid>` implements a highly reusable data grid to display your data.
Open `index.html` for the full element documentation

## Examples

### use remote data
To leverage the full capability of the grid, use it with remote data. This enables all features like searching, 
sorting, paging, ...
```
<dom-module id="your-element">
    <template>
        <actindo-grid id="grid"
                      remote="/your-endpoint"
                      items-per-page="25"
                      selection-mode="multi"
                      column-configuration="[[columns]]">
        </actindo-grid>
    </template>
    
    <script>
        class YourElement extends Polymer.Element {
            static get is() { return 'your-element'; }
            
            static get properties() {
                return {
                    columns: {
                        type: Array,
                        value: [
                            {
                                label: 'ID',
                                field: 'id',
                                type: Number,
                                identifying: true,
                                hidden: true
                            },
                            {
                                label: 'Name',
                                field: 'name',
                                type: String,
                                resizable: true,
                                searchable: true,
                                sortable: true
                            },
                            {
                                label: 'Status',
                                field: 'name',
                                type: Number,
                                resizable: true,
                                searchable: true,
                                sortable: true,
                                filterable: true,
                                defaultFilterProperties: {
                                    inputType: 'Option',
                                    items: [
                                        {
                                            id: '0',
                                            label: 'Inactive'
                                        },
                                        {
                                            id: '1',
                                            label: 'Active'
                                        }
                                    ]
                                }
                            },
                            {
                                label: 'active',
                                field: 'active',
                                type: Boolean,
                                sortable: true
                            }
                        ]
                    }
                };
            }
        }
        
        customElements.define(YourElement.is, YourElement); 
    </script>
</dom-module>
```


### Use local data (no remote)
While features are limited, you can still use the grid with local data only.
```
<dom-module id="your-element">
    <template>
        <actindo-grid id="grid"
                      items="[[data]]"
                      column-configuration="[[columns]]">
        </actindo-grid>
    </template>
    
    <script>
        class YourElement extends Polymer.Element {
            static get is() { return 'your-element'; }
            
            static get properties() {
                return {
                    columns: {
                        type: Array,
                        value: [
                            {
                                label: 'ID',
                                field: 'id',
                                type: Number,
                                identifying: true
                            },
                            {
                                label: 'Name',
                                field: 'name',
                                type: String
                            },
                            {
                                label: 'active',
                                field: 'active',
                                type: Boolean
                            }
                        ]
                    },
                    data: {
                        type: Array,
                        value: [
                            {id: 1, name: 'demo user 1', active: true},
                            {id: 2, name: 'demo user 2', active: false},
                            {id: 3, name: 'demo user 3', active: false},
                            {id: 4, name: 'demo user 4', active: true},
                            {id: 5, name: 'demo user 5', active: true},
                            {id: 6, name: 'demo user 6', active: false},
                        ]
                    }
                };
            }
        }
        
        customElements.define(YourElement.is, YourElement); 
    </script>
</dom-module>
```

### custom renderer 
Often, you will require custom data rendering for certain columns. This can be achived by passing a render
callback function to the column you wish to render manually. It is called with 2 parameters, the first is the 
value of the configured field, the second the entire object.
```
{
    label: 'Active',
    field: 'active',
    type: Boolean,
    render: function(value, row) { // has to return a DOMElement
        let element = document.createElement('paper-toggle-button');
        element.checked = value;
        
        return element;
    }
}
```

