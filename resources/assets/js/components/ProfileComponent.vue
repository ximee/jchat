<template>

    <div>

        <a v-on:click="showProfile()" class="dropdown-item custom-dropdown" href="javascript:void(0)">
            <i class="fas fa-user-circle"></i>
            <span>Profile</span>
        </a>


    </div>

</template>

<script>
    import swal from 'sweetalert';

    import moment from 'moment'

    export default {

        props: {
            self: {
                type: String,
                required: true,
            },
        },

        data() {
            return {
                myself: JSON.parse(this.self),
                content: '',
            }
        },


        mounted() {

            this.content = document.createElement('div');

            this.content.className='card';

            this.content.innerHTML = '<div class="card-body" style="display: flex;">' +
                                        '<img src="' + this.myself.avatar + '" ' + 'alt="Avatar" class="img-thumbnail">' +
                                        '<div>' +
                                            '<div class="alert alert-info" role="alert">' +
                                                '<span>name: ' + this.myself.name + '</span>' +
                                            '</div>' +
                                            '<div class="alert alert-info" role="alert">' +
                                                '<span>email: ' + this.myself.email + '</span>' +
                                            '</div>' +
                                            '<div class="alert alert-info" role="alert">' +
                                                '<span>online from: ' + this.getTime(this.myself.is_online) + '</span>' +
                                            '</div>' +
                                            '<div class="alert alert-info" role="alert">' +
                                                '<span>registered: ' + this.getTime(this.myself.registered) + '</span>' +
                                            '</div>'+
                                        '</div>' +
                                    '</div> ';
        },
        methods: {
            showProfile() {
                swal({
                    title: 'My Profile',
                    content: this.content,
                })

            },

            getTime(time) {
                if (moment(time).isValid()) {

                    return moment(time).format('DD.MM.YYYY, H:mm');
                }
            }
        }
    }

</script>