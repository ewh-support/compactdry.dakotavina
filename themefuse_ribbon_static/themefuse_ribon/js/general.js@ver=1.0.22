/*jQuery.get('https://themefuse.com/gumroad-params.php', function(data) {
    if( jQuery('.buy_now_btn').length > 0 ) {
        var _href = jQuery('body').find('.buy_now_btn').attr('href');
        var matches = _href.match(/^https?\:\/\/([^\/?#]+)(?:[\/?#]|$)/i);
        var domain = matches && matches[1];
        if (domain == 'gum.co')
            jQuery('body').find('.buy_now_btn').attr('href', _href + data);
    }
});*/

function getCookie(cname) {
    var name = cname + "=";
    var ca = document.cookie.split(';');
    for(var i = 0; i <ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0)==' ') {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length,c.length);
        }
    }
    return "";
}

// get a GET parameter
var getQueryParam = function(param) {
    var found;
    window.location.search.substr(1).split("&").forEach(function(item) {
        if (param ==  item.split("=")[0]) {
            found = item.split("=")[1];
        }
    });
    return found;
};
var iframe = getQueryParam('iframe');
//console.log(iframe);
if( iframe == 'true' ) {
    document.cookie = "demo_iframe=true";
}

// get demo_iframe cookie
var demo_iframe = getCookie('demo_iframe');
//console.log(demo_iframe);
if( demo_iframe == 'true' ){
    jQuery('head').append('<style>body:before{content: none !important;}</style>');
    jQuery('.tfuse-ribbon').remove();
    jQuery('body').removeClass('tf-static-ribbon-bar');
}
else {
    jQuery('.tfuse-ribbon').prependTo('body').addClass('animateIn');
}

// Detect Click in Iframe
function detectIframeClick() {
    var overiFrame = -1;
    var $ = jQuery;

    jQuery('#demo-iframe-holder').find('iframe').hover( function() {
        overiFrame = 1;
    }, function() {
        overiFrame = -1
    });
    jQuery(window).on('blur', function() {
        if( overiFrame != -1 ) {
            jQuery('#cuselBox').css('display', 'none');
            jQuery('.ribbon-cusel-select').removeClass('cuselOpen');
            jQuery('.colorpicker-wheel').addClass('hidden');
        }
    });
}

jQuery(window).load(function(){
    // move ribbon on the top, after body (for header 5,6)
    jQuery('.tfuse-ribbon').prependTo('body').addClass('animateIn');
});

// Demo Api
// --------------------------------------------------------------------------------- //
jQuery(document).ready(function($) {
    var $ = jQuery,
        screenWidth = jQuery(window).width(),
        screenHeight = jQuery(window).height(),
        intervalId;

    // Styling select for old theme
    function selectBoxit (){
        var selectTag = jQuery("#demo-panel #theme");

        selectTag.selectBoxIt();

        selectTag.bind({
            'open': function(){
                jQuery('html').css('overflow', 'hidden');
            },
            'close': function(){
                jQuery('html').css('overflow-y', 'scroll');
            }
        });
    }

    // Customize scrollBar in selectBox
    if(screenWidth > 1199){
        // Call styling function
        selectBoxit();

        // Styling Scroll Bar
        jQuery('.selectboxit-list').niceScroll({
            autohidemode: false,
            smoothscroll: true,
            cursorborder: "none",
            cursorwidth: "6px",
            cursorcolor: "#000",
            hwacceleration: false,
            cursorborderradius: "3px",
            railpadding: { top: 0, right: 2, left: 0, bottom: 10 }
        });
    }

    // Add <em> in selectBox Labels
    if (jQuery('.tfuse-ribbon .selectboxit-list .selectboxit-option .selectboxit-option-anchor').length > 0) {
        jQuery('.tfuse-ribbon .selectboxit-list .selectboxit-option .selectboxit-option-anchor, .tfuse-ribbon .selectboxit-container .selectboxit-text').each(function(){
            var $this = jQuery(this),
                text = $this.text().split('-');

            if(text[1]===undefined)
                $this.html(text[0]);
            else
                $this.html(text[0] + '<em>-' + text[1] + '</em>');
        });
    }

    // Customize scrollBar in dropDown lis demo
    if(screenWidth > 1199){
        jQuery('.demo-list').niceScroll({
            autohidemode: false,
            smoothscroll: true,
            cursorborder: "none",
            cursorwidth: "7px",
            cursoropacitymin: 0.7,
            cursoropacitymax: 0.2,
            cursorcolor: "#9aa0a3",
            cursorborderradius: "7px",
            railpadding: { top: 0, right: 10, left: 5, bottom: 10 }
        });
    }

    // Animate Button DemoList
    function animateButton(){
        var animateButtonsDemo = $('.demo-list-button');
        animateButtonsDemo.addClass('animate-button');

        setTimeout(function(){
            animateButtonsDemo.removeClass('animate-button');
        }, 1500);
    }
    animateButton();
    intervalId = setInterval(animateButton, 7000);

    // Open & Close Demo List
    jQuery('.demo-list-button').click(function(event){
        event.preventDefault();
        var button_demo_list = $(this),
            demo_list = $('.wrap-demo-list');

        // Open Function
        function openDemo(){
            demo_list.removeClass('close-list').addClass('open-list');
            button_demo_list.addClass('demo-button-open');
            button_demo_list.children('i').removeClass('tf-ribbon-icon-chevron-down').addClass('tf-ribbon-icon-chevron-up');
            jQuery('body').prepend('<div class="tfuse-ribbon-overlay-page"></div>');
            jQuery('html').css('overflow', 'hidden');
        }
        // Close Function
        function closeDemo(){
            demo_list.removeClass('open-list').addClass('close-list');
            button_demo_list.removeClass('demo-button-open');
            button_demo_list.children('i').removeClass('tf-ribbon-icon-chevron-up').addClass('tf-ribbon-icon-chevron-down');
            jQuery('.tfuse-ribbon-overlay-page').remove();
            jQuery('html').css('overflow-y', 'scroll');
        }
        // Open/Close Logical
        if(button_demo_list.next(demo_list).hasClass('close-list')){
            openDemo();
            clearInterval(intervalId);
        }
        else{
            closeDemo();
            intervalId = setInterval(animateButton, 7000);
        }
        // Close Demo List if Click Outside List
        jQuery('.tfuse-ribbon-overlay-page').click(function(event2){
            event2.preventDefault();
            closeDemo();
            intervalId = setInterval(animateButton, 7000);
        });
        // Close Demo List if Click on the bar
        jQuery("#demo-panel").click(function(event2){
            var target = jQuery( event2.target );
            if ( ! target.parents( ".demo-list-button-wrap" ).length ) {
                closeDemo();
                intervalId = setInterval(animateButton, 7000);
            }
        });
    });

    // Open Panel, Close Panel
    jQuery('#demo-panel-close').on('click', function(e) {
        e.preventDefault();
        jQuery('#demo-panel').addClass('closed');
        jQuery('#panelBack').removeClass('closed');
        jQuery('body').removeClass('panel-is-open').addClass('panel-is-close');
    });

    jQuery('#panelBack').on('click', function(e) {
        e.preventDefault();
        jQuery('#panelBack').addClass('closed');
        jQuery('#demo-panel').removeClass('closed');
        jQuery('body').removeClass('panel-is-close').addClass('panel-is-open');
    });

    detectIframeClick();

    jQuery('#demo-panel-close, #panelBack').on('click', function(){
        var demoPanelHeight = jQuery('#demo-panel').height(),
            screenHeight = jQuery(window).height();

        if(jQuery(this).parents('body').hasClass('panel-is-close')){
            jQuery('#demo-iframe-holder').css({
                'height': screenHeight
            });
        }
        else{
            jQuery('#demo-iframe-holder').css({
                'height': screenHeight - demoPanelHeight
            });
        }
    });

    // change theme in cusel select
    jQuery('#theme').on('change', function(){
        var val = jQuery(this).val();
        window.location.href = 'https://demo.themefuse.com/?theme='+val;
    });
});