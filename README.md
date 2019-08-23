# onchange-state-based-country-options
VIEW:

<div class=" col-md-4 mb">
                                            <select class="adj" name="district" id="mobileresultdistrict">
                                                <option value="0">- District selection -</option>
                                                <?php
                                                foreach ($districts as $key => $value) {
                                                    echo '<option value="' . $value->dist_id . '">' . strtoupper($value->dist_name) . '</option>';
                                                }
                                                ?>
                                            </select>
                                        </div>
                                        <div class=" col-md-4 mb">
                                            <select class="adj" name="mobileresultmandal" id="mobileresultmandal">
                                                <option value="">- mandal-selection -</option>
                                                                                             
                                            </select>
                                        </div>
SCRIPT:

$("#mobileresultdistrict").on('change', function () {
    var districtid = this.value;

    $.ajax({
        type: "POST",
        url: base_url + "districtmandal",
        type: "POST",
                data: {districtid: districtid},
        dataType: "json",
        success: function (response) {

            $('#mobileresultmandal').find('option').not(':first').remove();

//var cur_ques_details = response;

            $.each(response, function (index, data) {
//                 for (var i = 0; i < cur_ques_details.length; i++) {

                $('#mobileresultmandal').append('<option value="' + data['mandal_id'] + '">' + data['mandal_name'] + '</option>');
            });
//            }
        }

    })

});
