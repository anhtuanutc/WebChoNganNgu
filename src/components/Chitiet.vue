<template>
    <div class="modal">
        <div class="modal-container">

            <div class="modal-colse">
                <i class="las la-window-close" @click="Close()"></i>
            </div>
            <div class="modal-div">
                <i class="las la-newspaper"></i>
                Chi tiết đơn hàng
            </div>

            <div class="modal-body">
                <label for="" class="modal-label">
                    <i class="las la-user"></i>
                    Khách hàng:
                </label>

                <!-- // -->
                <div class="body-tr">
                    <tr>
                        <td>
                            <Label class="td-label">Mã:</Label>
                        </td>
                        <td>
                            <input type="text" class="tr-input" placeholder="Mã..." readonly v-model="this.data.MaTK">
                        </td>
                    </tr>
                    <br>
                    <tr>
                        <td>
                            <Label class="td-label">Tên:</Label>
                        </td>
                        <td>
                            <input type="text" class="tr-input" placeholder="Tên..." style="margin-left: 75px;" readonly
                                v-model="this.data.TenKH">
                        </td>
                    </tr>
                    <br>

                    <tr>
                        <td>
                            <Label class="td-label">Số điện thoại:</Label>
                        </td>
                        <td>
                            <input type="tel" class="tr-input" placeholder="Số điện thoại..." style="margin-left: 9px;"
                                readonly v-model="this.data.SDT">
                        </td>
                    </tr>
                </div>

                <!---->
                <label for="" class="modal-label">
                    <i class="las la-ticket-alt"></i>
                    Vé:
                </label>
                <div class="body-tr">
                    <tr>
                        <td>
                            <Label class="td-label">Thứ tự:</Label>
                        </td>
                        <td>
                            <input type="number" class="tr-input" style="margin-left: 54px;  width: 60px;" readonly
                                v-model="this.data.ThuTu">
                        </td>
                    </tr>

                    <tr>
                        <td>
                            <Label class="td-label" style="margin-left: 170px;">Số lượng:</Label>
                        </td>
                        <td>
                            <input type="number" class="tr-input" style="margin-left: 45px; width: 60px; " readonly
                                v-model="this.data.SoLuong">
                        </td>
                    </tr>
                    <br>

                    <tr>
                        <td>
                            <Label class="td-label">Loại vé:</Label>
                        </td>
                        <td>
                            <select name="Loai-ve" id="Loai-ve" style="margin-left: 50px;" disabled v-model="b">
                                <option value="null1" disabled>{{ this.data.Ten }}</option>
                            </select>
                        </td>
                    </tr>

                </div>

                <!-- <-- -->
                <label for="" class="modal-label">
                    <i class="las la-calendar-times"></i>
                    Buổi diễn:
                </label>

                <div class="body-tr">
                    <tr>
                        <td>
                            <Label class="td-label">Địa điểm:</Label>
                        </td>
                        <td>
                            <input type="text" class="tr-input" placeholder="Địa điểm..." style="margin-left: 38px;"
                                readonly v-model="this.data.DiaDiem">
                        </td>
                    </tr>
                    <br>
                    <tr>
                        <td>
                            <Label class="td-label">Thời gian:</Label>
                        </td>
                        <td>
                            <input type="date" class="tr-input" placeholder="Thời gian..." style="margin-left: 34px;"
                                readonly v-model="this.data.ThoiGian">
                        </td>
                    </tr>
                    <br>

                    <tr>
                        <td><Label class="td-label">Trạng thái:</Label></td>
                        <td>
                            <form action="" class="from-td">
                                <input type="radio" style="margin-right: 15px;"  value="Da thanh toan" v-model="this.data.TrangThai" />Đã thanh toán
                                <br>
                                <input type="radio" value="Chua thanh toan" style="margin-right: 15px; margin-top: 15px;" v-model="this.data.TrangThai"/>Chưa thanh
                                toán
                            </form>
                        </td>
                    </tr>
                </div>

                <!-- <-- -->
                <label for="" class="modal-label">
                    <i class="las la-money-bill"></i>
                    Tổng tiền: <input type="text" class="modal-input" placeholder="Tổng tiền..."
                        style="margin-left: 115px;" readonly v-model="this.data.TongTien">
                </label>

                <label for="" class="modal-label">
                    <i class="las la-user-astronaut"></i>
                    Mã nhân viên: <input type="text" class="modal-input" placeholder="Mã Nhân viên..."
                        style="margin-left: 85px;" readonly v-model="this.data.MaNhanVien">
                </label>

                <!-- <-- -->
                <div class="modal-time">
                    <tr>
                    <tr>
                        <td>

                            <Label>
                                <i class="las la-money-bill"></i>Thời gian:
                            </Label>
                        </td>
                        <td>
                            <input type="date" class="tr-input" placeholder="Thời gian..."
                                style="margin-left: 97px; margin-right: 15px;" readonly
                                v-model="this.data.Thoigianlaphoadon">
                        </td>
                    </tr>
                    </tr>
                </div>

                <button id="btl-them">Thêm</button>
                <button id="btl-sua">Sửa</button>
                <button id="btl-xoa">Xóa</button>
            </div>
        </div>
    </div>
</template>
<script>
import axios from "axios";
import moment from "moment";
export default {
    props: ["ID"],
    data() {
        return {
            data: {},
            b:"null1"
        }
    },
    created: function () {
        this.List(this.ID);

    },
    methods: {
        /**
         * Call dữ liệu về
         * Author: Lợn Cọc
         * Date: 18:28 26/12/2022
         */
        List(id) {
            try {
                axios.get("http://localhost:8080/LaytheoId?id=" + id).then((response) => {
                    this.data = response.data;
                    this.data.ThoiGian = this.format_date(this.data.ThoiGian);
                    this.data.Thoigianlaphoadon = this.format_date(this.data.Thoigianlaphoadon);
                });
            } catch (error) {
                console.log(error);
            }
        },
        /**
         * Định dạng ngày tháng năm 
         * Author: Lợn Cọc
         * Date : 18:28 26/12/2022
         */
        format_date(value) {
            try {
                if (value) {
                    return moment(String(value)).format("YYYY-MM-DD");
                }
            } catch (error) {
                console.log(error);
            }
        },
        /**
         * Đóng chi tiết đơn
         * Author: Lợn Cọc
         * Date: 18:28 26/12/2022
         */
        Close() {
            this.$emit("CloseChiTiet", false);
        }
    }
}
</script>