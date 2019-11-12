<page class="page">
	<actionBar title="CSS Colors Game!" class="action-bar">
	</actionBar>
	<stackLayout>
        <label id="streak" text="Streak: {streak}"  />
        <label id="timer" text="Timer: {time}"  />
		<label id="question-circle" alignSelf="center" text="What color is {targetColor}?" />
		<gridLayout alignSelf="center" columns="*, *" rows="*, *">
			<label on:tap={() => choose(colors[0])} row="0" col="0" backgroundColor={colors[0]}/>
			<label on:tap={() => choose(colors[1])} row="0" col="1" backgroundColor={colors[1]}/>
			<label on:tap={() => choose(colors[2])} row="1" col="0" backgroundColor={colors[2]}/>
			<label on:tap={() => choose(colors[3])} row="1" col="1" backgroundColor={colors[3]}/>
		</gridLayout>
	</stackLayout>
</page>

<style>
    gridLayout {
        width: 100%;
    }
    gridLayout > label {
        margin: 10;
        font-size: 20;
        font-weight: bold;
        text-align: center;
        border-color: black;
        border-style: solid;
        border-width: 2;
    }

    #streak, #timer {
        font-size: 20;
        text-align: center;
        background-color: yellow;
    }

    #question-circle {
        border-radius: 100%;
        height: 200;
        padding: 80 0;
        font-size: 20;
        text-align: center;
    }

</style>

<script>
    import {showModal} from 'svelte-native';
    import LosePage from './LosePage.svelte';
    let allColors = [
            'IndianRed','LightCoral','Salmon','DarkSalmon','LightSalmon','Crimson','Red','FireBrick','DarkRed','Pink','LightPink','HotPink','DeepPink','MediumVioletRed','PaleVioletRed','Coral','Tomato','OrangeRed','DarkOrange','Orange','Gold','Yellow','LightYellow','LemonChiffon','LightGoldenrodYellow','PapayaWhip','Moccasin','PeachPuff','PaleGoldenrod','Khaki','DarkKhaki','Lavender','Thistle','Plum','Violet','Orchid','Fuchsia','Magenta','MediumOrchid','MediumPurple','BlueViolet','DarkViolet','DarkOrchid','DarkMagenta','Purple','RebeccaPurple','Indigo','MediumSlateBlue','SlateBlue','DarkSlateBlue','GreenYellow','Chartreuse','LawnGreen','Lime','LimeGreen','PaleGreen','LightGreen','MediumSpringGreen','SpringGreen','MediumSeaGreen','SeaGreen','ForestGreen','Green','DarkGreen','YellowGreen','OliveDrab','Olive','DarkOliveGreen','MediumAquamarine','DarkSeaGreen','LightSeaGreen','DarkCyan','Teal','Aqua','Cyan','LightCyan','PaleTurquoise','Aquamarine','Turquoise','MediumTurquoise','DarkTurquoise','CadetBlue','SteelBlue','LightSteelBlue','PowderBlue','LightBlue','SkyBlue','LightSkyBlue','DeepSkyBlue','DodgerBlue','CornflowerBlue','RoyalBlue','Blue','MediumBlue','DarkBlue','Navy','MidnightBlue','Cornsilk','BlanchedAlmond','Bisque','NavajoWhite','Wheat','BurlyWood','Tan','RosyBrown','SandyBrown','Goldenrod','DarkGoldenrod','Peru','Chocolate','SaddleBrown','Sienna','Brown','Maroon','White','Snow','Honeydew','MintCream','Azure','AliceBlue','GhostWhite','WhiteSmoke','Seashell','Beige','OldLace','FloralWhite','Ivory','AntiqueWhite','Linen','LavenderBlush','MistyRose','Gainsboro','LightGray','LightGrey','Silver','DarkGray','DarkGrey','Gray','Grey','DimGray','DimGrey','LightSlateGray','LightSlateGrey','SlateGray','SlateGrey','DarkSlateGray','DarkSlateGrey','Black'
        ]

    let streak = 0;
    let time = 10;

    function setTimerInterval() {
        return setInterval(() => {
            time--;
            if (time === 0) {
                lose();
            }
        }, 1000);
    }

    let intervalId = setTimerInterval();

    let colors = [
        allColors[randomInt(allColors.length)],
        allColors[randomInt(allColors.length)],
        allColors[randomInt(allColors.length)],
        allColors[randomInt(allColors.length)]
    ];

    let targetColor = colors[randomInt(4)];

    function randomInt(n) {
        return Math.floor(Math.random() * n)
    }

    async function lose() {
        time = 10;
        streak = 0;
        clearInterval(intervalId);
        await showModal({page: LosePage});
        randomize();
        intervalId = setTimerInterval();
    }

    function choose(color) {
        if (color === targetColor) {
            streak += 1;
            time += 1;
            randomize();
        } else {
            lose();
        }
    }

    function randomize() {
        colors = [
            allColors[randomInt(allColors.length)],
            allColors[randomInt(allColors.length)],
            allColors[randomInt(allColors.length)],
            allColors[randomInt(allColors.length)]
        ];

        targetColor = colors[randomInt(4)];
    }
</script>