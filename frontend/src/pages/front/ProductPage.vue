<template>
    <div class="product-page">
        <div class="on__top">
            <div class="top_content">
                <div class="page-title">Products</div>
                <q-input dense v-model="filterr" outlined label="Search for keywords"/>
            </div>
            <div class="for_balance"></div>
        </div>
        <div class="table-w-form">
            <div class="left">
                <q-table
                :rows="rows"
                :columns="columns"
                row-key="name"
                separator="cell"
                binary-state-sort
                :pagination="pagination"
                :filter="filterr"
                >
                <template v-slot:body-cell-action="props">
                    <q-td :props="props" class="actions">
                        <q-btn class="q-mr-sm" @click="editData(props.row)" dense no-caps flat label="Edit"/>
                        <q-btn dense no-caps @click="deleteData(props.row.id)" flat label="Delete"/>
                    </q-td>
                </template>
                </q-table>
                <div class="grid-table">
                    <div class="table-item" v-for="(item,  index) in rows" :key="index">
                        <div class="w__name_price">
                            <div class="label">Name</div>
                            <div class="Value">{{ item.name }}</div>
                            <div class="label">Price</div>
                            <div class="Value">{{ item.price }}</div>
                        </div>
                        <div class="actions">
                            <q-btn flat label="Edit" @click=editDataOnDialog(item) />
                            <q-btn flat label="delete" @click="deleteData(item.id)"/>
                        </div>
                    </div>
                </div>
            </div>
            <div class="right">
                <q-form @submit.prevent="submitFrom()">
                    <div class="header">
                        <div class="header-text">Header Text</div>
                        <div class="header-desc">
                            Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam!
                        </div>
                    </div>
                    <div class="form-action">
                        <q-input dense bg-color="white" standout="bg-black"  v-model="form_data.name" label="Name"/>
                        <q-input dense bg-color="white" standout="bg-black" v-model="form_data.price" label="Price"/>
                        <q-btn no-caps flat type="submit" :label="edit_data ? 'Save': 'Create'"/>
                    </div>
                </q-form>
            </div>
        </div>
        <q-dialog v-model="open_edit_dialog">
            <q-card>
                <q-card-section>
                    <q-form @submit.prevent="submitFrom()">
                        <div class="header">
                            <div class="header-text">Header Text</div>
                            <div class="header-desc">
                                Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam!
                            </div>
                        </div>
                        <div class="form-action">
                            <q-input dense bg-color="white" standout="bg-black"  v-model="form_data.name" label="Name"/>
                            <q-input dense bg-color="white" standout="bg-black" v-model="form_data.price" label="Price"/>
                            <q-btn no-caps flat type="submit" :label="edit_data ? 'Save': 'Create'" v-close-popup/>
                        </div>
                    </q-form>
                </q-card-section>
            </q-card>
        </q-dialog>
    </div>
</template>

<script>
export default
{
    filters: { },
    data:() =>(
    {
        open_edit_dialog: false,
        edit_data: false,
        filterr: null,
        pagination: { rowsPerPage: 10 },
        form_data:
        {
            name: null,
            price: null,
        },
        rows:
        [
            {
                id: 1001,
                name:'Lorem ipsum',
                price:'Lorem ipsum'
            },
            {
                id: 1002,
                name:'Lorem ipsum',
                price:'Lorem ipsum'
            },
            {
                id: 1003,
                name:'Lorem ipsum',
                price:'Lorem ipsum'
            },
            {
                id: 1004,
                name:'Lorem ipsum',
                price:'Lorem ipsum'
            },
            {
                id: 1005,
                name:'Lorem ipsum',
                price:'Lorem ipsum'
            },
            {
                id: 1006,
                name:'Lorem ipsum',
                price:'Lorem ipsum'
            },
            {
                id: 1007,
                name:'Lorem ipsum',
                price:'Lorem ipsum'
            },
            {
                id: 1008,
                name:'Lorem ipsum',
                price:'Lorem ipsum'
            },

        ],
        columns:
        [
            {
                name: 'name',
                required: true,
                label: 'name',
                align: 'center',
                field: row => row.name,
                format: val => `${val}`,
            },
            {
                name: 'price',
                required: true,
                label: 'price',
                align: 'center',
                field: row => row.price,
                format: val => `${val}`,
            },
            {
                name: 'action',
                label: 'action',
                align: 'center',

            },
        ]
    }),
    mounted() { },
    methods:
    {
        submitFrom()
        {
            this.$q.loading.show();
            if (this.edit_data === true) 
            {
                let new_rows_data = [];
                for (let i = 0; i < this.rows.length; i++) 
                {
                    const element = this.rows[i];
                    if (element.id === this.form_data.id) 
                    {
                        element.name = this.form_data.name;
                        element.price = this.form_data.price;
                    }
                    new_rows_data.push(element);
                }
                this.rows = new_rows_data;
                this.form_data={ name: null, price: null };
            }
            else 
            {
                let last_el = this.rows[this.rows.length - 1];
                this.form_data.id = last_el.id + 1;
                this.rows.push(this.form_data);
                this.form_data={ name: null, price: null }
            }
            this.$q.loading.hide();
            this.$q.dialog({title: this.edit_data ? 'Saved' : 'Created', message: 'Table has been updated.'});
            this.edit_data = false;
        },
        editData(data)
        {
            this.edit_data = true;
            this.form_data.name = data.name;
            this.form_data.price = data.price;
            this.form_data.id = data.id;
        },
        editDataOnDialog(data)
        {
            this.open_edit_dialog = true;
            this.editData(data);
        },
        deleteData(id)
        {
            this.$q.loading.show();
            this.rows = this.rows.filter(row => row.id != id)
            this.$q.loading.hide();
            this.$q.dialog({title: 'Deleted', message: 'Data has been deleted.'})
        }
    },
    computed: { }
}
</script>