<template>
    <div class="messanger">
        <div class="chatlist">
            <div class="chatlist__item">
                <div>
                    <span>alex.ivanov@gmail.com</span>
                    <small>14:47</small>
                </div>
                <p>Lorem Ipsum Lorem Ipsum Lorem Ipsum Lorem Ipsum</p>
            </div>
        </div>

        <div class="chatbox">
            <div class="chatbox__header">
                <h1>alex.ivanov@gmail.com</h1>
            </div>
            <div class="chatbox__body">
                <div class="message__form" ref="messageContainer">
                    <div class="message__to">
                        <div>
                            <div class="message">
                                <div class="message__item to">
                                    <p class="mb-0">Сообщение</p>
                                </div>
                                <div class="time text-right">
                                    <small>15:02</small>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="message__to">
                        <div>
                            <div class="message">
                                <div class="message__item to">
                                    <p class="mb-0">Сообщение</p>
                                </div>
                                <div class="time text-right">
                                    <small>15:02</small>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
            <div class="chatbox__footer">
                <input type="text" class="w-100" placeholder="Введите сообщение...">
                <div class="send">
                    <img src="@/assets/img/send.svg" alt="" loading="lazy">
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {

        }
    }
}
</script>
<script setup>
useSeoMeta({
    title: 'Мессенджер | Studynow',
    ogTitle: 'Мессенджер | Studynow',
    description: 'Мессенджер | Studynow',
    ogDescription: 'Мессенджер | Studynow',
})
</script>
<style lang="scss" scoped>
.messanger {
    margin-top: 34px;
    display: flex;
    gap: 30px;

    .chatbox {
        border-radius: 10px;
        background: #FFF;
        box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
        padding: 20px 40px;
        width: 100%;

        .chatbox__footer {
            display: flex;
            gap: 20px;

            .send {
                padding: 9px 13px;
                border-radius: 10px;
                border: 2px solid #000;
                display: flex;
                align-items: center;
                cursor: pointer;
            }

            input {
                border-radius: 10px;
                border: 2px solid #000;
                background: transparent;
                padding: 16px 30px;

                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 110%;
                font-family: var(--int);
                color: #000;
            }
        }

        .chatbox__body {
            .message__from {
                display: flex;
            }

            .message__to {
                display: flex;
                justify-content: flex-end;
            }

            .message__item p {
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
            }

            .message small {
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: 130%;
                font-family: var(--int);
                color: #000;
            }

            .message__form {
                margin-top: 45px;
                height: 468px;
                overflow: auto;
            }

            .message__form::-webkit-scrollbar {
                width: 0px;
                height: 0px;
            }

            .from {
                border-radius: 10px 10px 10px 0px;
            }

            .to {
                border-radius: 10px 10px 0 10px;
            }

            .message__item {
                padding: 20px;
                border: 2px solid #000;
                max-width: 543px;
                margin-bottom: 5px;
            }

            .message {
                margin-bottom: 51px;
            }
        }
    }

    .chatlist {
        display: flex;
        flex-direction: column;
        gap: 20px;

        .chatlist__item {
            border-radius: 10px;
            background: #FFF;
            box-shadow: 0px 0px 15px 0px rgba(0, 0, 0, 0.10);
            cursor: pointer;
            padding: 20px;
            width: 29.167vw;

            div {
                display: flex;
                justify-content: space-between;
                margin-bottom: 14px;

                span {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 500;
                    line-height: normal;
                    font-family: var(--int);
                    color: #000;
                }

                small {
                    font-size: 20px;
                    font-style: normal;
                    font-weight: 400;
                    line-height: 130%;
                    font-family: var(--int);
                    color: #000;
                }
            }

            p {
                margin: 0;
                font-size: 16px;
                font-style: normal;
                font-weight: 400;
                line-height: normal;
                font-family: var(--int);
                color: rgba(0, 0, 0, 0.70);
            }
        }
    }
}
</style>