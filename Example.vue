<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8 col-md-offset-2">
                <div class="panel panel-default">
                    <div class="panel-heading">Example Component</div>

                    <div class="panel-body">
                        Hello {{ user.name }}<br>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                'user': {},
            };
        },
        mounted() {
            axios.get('/api/user')
            .then((response) => {
                this.user = response.data;
            });
        },
    }
</script>
