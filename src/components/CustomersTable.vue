<template>
    <el-table
            ref="filterTable"
            :data="ordersData"
            style="width: 100%">
        <el-table-column
                prop="date_added"
                label="Date Added"
                sortable
                width="200"
                column-key="date_added"
        >
        </el-table-column>
        <el-table-column
                prop="customer_id"
                label="Customer ID"
                sortable
                width="200">
        </el-table-column>
        <el-table-column
                prop="customer_name"
                label="Customer Name"
                sortable
                width="200">
        </el-table-column>
        <el-table-column
                prop="poster_variable"
                label="Poster Variable"
                sortable
                width="200">
        </el-table-column>
        <el-table-column
                prop="poster_preview"
                label="Poster preview"
                width="200"
        >
        <template slot-scope="props">
            <el-button type="text" @click="goTo(props.row.poster_preview)">Click to preview poster</el-button>
        </template>
        </el-table-column>
        <el-table-column
                prop="generate_poster"
                label="Generate poster"
                width="200">
        <template slot-scope="scope">
            <el-button type="primary" :loading="loading_generate" @click="generatePoster(34799, 8400, 12000 )">Generate poster</el-button>
        </template>
        </el-table-column>
        <el-table-column
                prop="download_file"
                label="Download file"
                width="200">
            <template slot-scope="scope">
                <el-button type="success" :loading="loading_download" @click="downloadFile('http://3a2.7a4.myftpupload.com/wp-content/themes/storefront/Poster/assets/images/Artfor34799wall.jpeg')">Download file</el-button>
            </template>
        </el-table-column>
        <el-table-column
                prop="send_to_customer"
                label="Send to Customer"
                width="200">
            <template slot-scope="scope">
                <el-button type="info" :loading="loading_send" @click="sendToCustomer(scope.row.customer_id, 34799, 8400, 12000 )">Send to customer</el-button>
            </template>
        </el-table-column>
        <el-table-column
                prop="mark_complete"
                label="Mark Complete"
                width="200">
            <template slot-scope="scope">
                <el-button type="warning" :loading="loading_move" @click="moveToComplete(scope.row.customer_id)">Mark Complete</el-button>
            </template>
        </el-table-column>

    </el-table>
</template>

<script>
    /* eslint-disable no-console */

    const axios = require('axios');
    export default {
        name: "CustomersTable",
        props: ["ordersData"],
        data() {
            return {
                loading_generate: false,
                loading_download: false,
                loading_send: false,
                loading_move: false,
                headers: {
                    "Access-Control-Allow-Origin": "*",
                }
            }
        },
        methods: {
            formatter(row) {
                return row.address;
            },
            filterTag(value, row) {
                return row.tag === value;
            },
            goTo(webLocation) {
                window.open(webLocation, '_blank');
            },
            generatePoster(postercode , posterwidth , posterheight)
            {
                this.loading_generate = true;
                axios.post('http://artsforwall.co.uk/formdata/',
                        {'genrt_postercode': postercode ,
                        'genrt_posterwirth': posterwidth ,
                        'genrt_posterheight': posterheight
                        }, this.headers)
                    .then(function (response) {
                        console.log(response);
                    })
                    .catch(function (error) {
                        console.log(error);
                    });
            },
            downloadFile(link) {
                window.open(link, 'Download');
            },
            sendToCustomer (getorder_id , poster_code_url , url_postre_width , url_poster_height)
            {
                this.loading_send = true;
                axios.post('http://artsforwall.co.uk/formdata/',
                    {'sendtocustomer': getorder_id , 'poster_code_ema': poster_code_url , 'poster_width': url_postre_width , 'poster_height': url_poster_height}, this.headers)
                    .then(function (response) {
                        console.log(response);
                    })
                    .catch(function (error) {
                        console.log(error);
                    });
            },
            moveToComplete(orderid)
            {
                this.loading_move = true;
                axios.post('http://artsforwall.co.uk/formdata/',
                    {'movetocomplete': orderid }, this.headers)
                    .then(function (response) {
                        console.log(response);
                    })
                    .catch(function (error) {
                        console.log(error);
                    });
            }
    }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .el-row {
        margin-bottom: 20px;
        &:last-child {
            margin-bottom: 0;
        }
    }
    .el-col {
        border-radius: 4px;
    }
    .bg-purple-dark {
        background: #bfad7e;
    }
    .bg-purple {
        background: #76e62e;
    }
    .bg-purple-light {
        background: #6577f2;
    }
    .grid-content {
        border-radius: 4px;
        min-height: 36px;
    }
    .row-bg {
        padding: 10px 0;
        background-color: #5cfccf;
    }
</style>
