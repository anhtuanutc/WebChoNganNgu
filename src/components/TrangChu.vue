<template>
    <div class="main">
        <div class="sidebar">
            <div class="sidebar-brand">
                <h2> <span class="las la-heart"></span> BlackPink </h2>
            </div>

            <div class="siderbar-menu">
                <ul>
                    <li>
                        <a href="" class="active"><span class="las la-home"></span>
                            <span>Trang chủ</span></a>
                    </li>
                    <li>
                        <a href=""><span class="las la-ticket-alt"></span>
                            <span>Quản lý vé</span></a>
                    </li>
                    <li>
                        <a href=""><span class="las la-people-carry"></span>
                            <span>Quản lý khách hàng</span></a>
                    </li>
                    <li>
                        <a href=""><span class="las la-receipt"></span>
                            <span>Quản lý đơn hàng</span></a>
                    </li>
                    <li>
                        <a href=""><span class="las la-microphone-alt"></span>
                            <span>Quản lý nhóm nhạc</span></a>
                    </li>
                    <li>
                        <a href=""><span class="las la-clipboard-list"></span>
                            <span>Báo cáo doanh thu</span></a>
                    </li>
                    <li>
                        <a href=""><span class="lab la-whmcs"></span>
                            <span>Cài đặt</span></a>
                    </li>
                </ul>
            </div>
        </div>

        <div class="main-header">
            <header>
                <h2 class="bars">
                    <label for="">
                        <span class="las la-bars"></span>
                    </label>
                </h2>

                <div class="search-wrapper">
                    <span class="las la-search"></span>
                    <input type="search" placeholder="Search here" />
                </div>

                <div class="user-wrapper">
                    <img src="../assets/img/img2.jpg" width="40px" height="40px" alt="">
                    <div>
                        <h4>Jennie</h4>
                        <small>Supper admin</small>
                    </div>
                </div>
            </header>

            <main>

                <div class="page-content">
                    <div class="analytice">
                        <div class="cards">
                            <div class="cards-single">
                                <div>
                                    <h1>54</h1>
                                    <span>Vé đã bán</span>
                                </div>
                                <div>
                                    <span class="las la-ticket-alt"></span>
                                </div>
                            </div>


                            <div class="cards-single">
                                <div>
                                    <h1>79</h1>
                                    <span>Người xem</span>
                                </div>
                                <div>
                                    <span class="las la-clipboard"></span>
                                </div>
                            </div>


                            <div class="cards-single">
                                <div>
                                    <h1>124</h1>
                                    <span>Đơn hàng</span>
                                </div>
                                <div>
                                    <span class="las la-shopping-bag"></span>
                                </div>
                            </div>


                            <div class="cards-single">
                                <div>
                                    <h1>$5k</h1>
                                    <span>Doanh thu</span>
                                </div>
                                <div>
                                    <span class="lab la-google-wallet"></span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="records">
                        <div class="slider-records">
                            <div class="add">
                                <span>Mục lục</span>
                                <select name="" id="">
                                    <option value="">Mã</option>
                                </select>
                                <button>Thêm thông tin</button>
                            </div>

                            <div class="slider-browse">
                                <input type="search" placeholder="Search" class="record-search">
                                <select name="" id="">
                                    <option value="">Mục lục</option>
                                </select>
                            </div>
                        </div>
                        <div class="table-responsive">
                            <table width="100%">
                                <thead>
                                    <tr >
                                        <th>Mã khách hàng</th>
                                        <th>Tên khách hàng</th>
                                        <th>Địa điểm</th>
                                        <th>Tổng tiền</th>
                                        <th>Thời gian tạo</th>
                                        <th>Trạng thái</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <!-- <-- -->
                                    <tr v-for="data in datas" :key="data.SoHoaDon">
                                        <td>0{{data.MaTK}}</td>
                                        <td>
                                            <div class="client">
                                                <h4>{{ data.TenKH }}</h4>
                                                <small>{{ data.SDT }}</small>
                                            </div>
                                        </td>
                                        <td>{{ data.DiaDiem }}</td>
                                        <td>{{data.TongTien}}$</td>
                                        <td>{{ format_date(data.Thoigianlaphoadon) }}</td>
                                        <td>
                                            <div class="actions">
                                                <span class="las la-trash"></span>
                                                <span class="las la-eye"></span>
                                                <span class="las la-ellipsis-v"></span>
                                                <button @click="Show(data.SoHoaDon)">Chi tiết</button>
                                            </div>
                                        </td>
                                    </tr>
                                    <!-- <-- -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </main>
        </div>
    </div>
</template>
<script>
import axios from "axios";
import moment from "moment";
export default {
    data() {
        return {
            datas: []
        }
    },
    created: function () {
        this.List();
    },
    methods: {
        List() {
            try {
                axios.get("http://localhost:8080/Layds").then((response) => {
                    this.datas = response.data;
                });
            } catch (error) {
                console.log(error);
            }
        },
        format_date(value) {
            try {
                if (value) {
                    return moment(String(value)).format("DD/MM/YYYY");
                }
            } catch (error) {
                console.log(error);
            }
        },
        Show(id){
            this.$emit("ShowChiTiet",true,id);
        }
    }
}
</script>