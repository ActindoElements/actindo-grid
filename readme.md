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
                      data="[[data]]"
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
                                resiable: true,
                                searchable: true,
                                sortable: true
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
                      data="[[data]]"
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
callback function to the column you wish to manually render
```
{
    label: 'Active',
    field: 'active',
    type: Boolean,
    render: function(row, column) { // has to return a DOMElement
        let element = document.createElement('paper-toggle-button');
        element.checked = row[column.field];
        
        return element;
    }
}
```

