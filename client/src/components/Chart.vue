<template>
    <article class="h-fit w-full flex flex-col">
        <div class="w-full h-fit flex items-center">
            <p class="h-fit transform rotate-180 text-xs" style="writing-mode: vertical-rl;">Level
                (Centimeter)</p>
            <div class="flex-1" id="water-level-chart"></div>
        </div>
        <p class="text-center text-xs text-black">Waktu (Second)</p>
    </article>
</template>

<script>
window.addEventListener('load', () => {
    // Apex Single Area Chart
    (function () {
        buildChart('#water-level-chart', (mode) => ({
            chart: {
                height: 300,
                type: 'area',
                toolbar: {
                    show: false
                },
                zoom: {
                    enabled: false
                }
            },
            series: [
                {
                    name: 'Visitors',
                    data: [0, 51, 60, 38, 40, 50, 40, 52, 65, 69, 60, 69]
                }
            ],
            legend: {
                show: false
            },
            dataLabels: {
                enabled: false
            },
            stroke: {
                curve: 'smooth',
                width: 3
            },
            grid: {
                strokeDashArray: 2
            },
            fill: {
                type: 'gradient',
                gradient: {
                    type: 'vertical',
                    shadeIntensity: 1,
                    opacityFrom: 0.1,
                    opacityTo: 0.8
                }
            },
            xaxis: {
                type: 'category',
                tickPlacement: 'on',
                categories: [
                    '25 January 2023',
                    '26 January 2023',
                    '27 January 2023',
                    '28 January 2023',
                    '29 January 2023',
                    '30 January 2023',
                    '31 January 2023',
                    '1 February 2023',
                    '2 February 2023',
                    '3 February 2023',
                    '4 February 2023',
                    '5 February 2023'
                ],
                axisBorder: {
                    show: false
                },
                axisTicks: {
                    show: false
                },
                crosshairs: {
                    stroke: {
                        dashArray: 0
                    },
                    dropShadow: {
                        show: false
                    }
                },
                tooltip: {
                    enabled: false
                },
                labels: {
                    style: {
                        colors: '#9ca3af',
                        fontSize: '13px',
                        fontFamily: 'Fredoka, ui-sans-serif',
                        fontWeight: 400
                    },
                    formatter: (title) => {
                        let t = title;

                        if (t) {
                            const newT = t.split(' ');
                            t = `${newT[0]} ${newT[1].slice(0, 3)}`;
                        }

                        return t;
                    }
                }
            },
            yaxis: {
                max: 70,
                labels: {
                    align: 'left',
                    minWidth: 0,
                    maxWidth: 140,
                    style: {
                        colors: '#9ca3af',
                        fontSize: '13px',
                        fontFamily: 'Fredoka, ui-sans-serif',
                        fontWeight: 400
                    },
                    formatter: (value) => value >= 1000 ? `${value / 1000}k` : value
                }
            },
            tooltip: {
                x: {
                    format: 'MMMM yyyy'
                },
                y: {
                    formatter: (value) => `${value >= 1000 ? `${value / 1000}k` : value}`
                },
                custom: function (props) {
                    const { categories } = props.ctx.opts.xaxis;
                    const { dataPointIndex } = props;
                    const title = categories[dataPointIndex].split(' ');
                    const newTitle = `${title[0]} ${title[1]}`;

                    return buildTooltip(props, {
                        title: newTitle,
                        mode,
                        valuePrefix: '',
                        hasTextLabel: true,
                        markerExtClasses: '!rounded-sm',
                        wrapperExtClasses: 'min-w-28'
                    });
                }
            },
            responsive: [{
                breakpoint: 568,
                options: {
                    chart: {
                        height: 300
                    },
                    labels: {
                        style: {
                            colors: '#9ca3af',
                            fontSize: '11px',
                            fontFamily: 'Fredoka, ui-sans-serif',
                            fontWeight: 400
                        },
                        offsetX: -2,
                        formatter: (title) => title.slice(0, 3)
                    },
                    yaxis: {
                        labels: {
                            align: 'left',
                            minWidth: 0,
                            maxWidth: 140,
                            style: {
                                colors: '#9ca3af',
                                fontSize: '11px',
                                fontFamily: 'Fredoka, ui-sans-serif',
                                fontWeight: 400
                            },
                            formatter: (value) => value >= 1000 ? `${value / 1000}k` : value
                        }
                    },
                },
            }]
        }), {
            colors: ['#2563eb', '#9333ea'],
            fill: {
                gradient: {
                    stops: [0, 90, 100]
                }
            },
            xaxis: {
                labels: {
                    style: {
                        colors: '#9ca3af'
                    }
                }
            },
            yaxis: {
                labels: {
                    style: {
                        colors: '#9ca3af'
                    }
                }
            },
            grid: {
                borderColor: '#e5e7eb'
            }
        }, {
            colors: ['#3b82f6', '#a855f7'],
            fill: {
                gradient: {
                    stops: [100, 90, 0]
                }
            },
            xaxis: {
                labels: {
                    style: {
                        colors: '#a3a3a3',
                    }
                }
            },
            yaxis: {
                labels: {
                    style: {
                        colors: '#a3a3a3'
                    }
                }
            },
            grid: {
                borderColor: '#404040'
            }
        });
    })();
});

export default {
    name: "Chart",
};
</script>