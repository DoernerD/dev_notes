# LaTeX Notes

Everything I look up way too often when writing in LaTeX

## Figures

Displaying two figures next to each other: Use the caption and subcaption package. Subcaption provides a subfigure environment, works quite nice.
MWE:
    \usepackage{caption}
    \usepackage{subcaption}

    \begin{figure}[htbp]
        \centering
        \begin{subfigure}{0.5\textwidth}
            \centering
            \includegraphics[width=0.75\linewidth]{figures/erdos-renyi_plot_diffusion.png}
            \caption{Diffusion Trend of the Erdos-Renyi graph.}
        \label{fig:er_diff}
        \end{subfigure}%
        \begin{subfigure}{0.5\textwidth}
            \centering
            \includegraphics[width=0.75\linewidth]{figures/erdos-renyi_plot_prevalence.png}
            \caption{Prevalence of the Erdos-Renyi graph.}
        \label{fig:er_prev}
        \end{subfigure}
        \caption{Solution for the Erdos-Renyi Graph.}
        \label{fig:er}
    \end{figure}

Note that subcaption doesn't work together with the subfig package. There's a debate
which one is better. Subcaption works nicely though.

### creating tikz figures

Use the standalone package from latex to create tikz figures. Put them all in one folder to collect them.
Then use a make file to compile them individually and clean up afterwards. The idea is to only have the tex
files and the make file in the folder and only compile if needed.
    -> figure out how to hand an argument to a make file
    -> Can you directly use the tikz file or do you need to remove the headers and stuff? 
        => Yep, you can. You only need to add \usepackage{standalone} in the preamble of the document where 
           you want to use the tikz file. Super convenient.
    -> Can you call the make file directly from vim?

## Resizing stuff

To make a table fit to textwidth easily
thanks https://tex.stackexchange.com/questions/27097/changing-the-font-size-in-a-table

    \documentclass{article}
    \usepackage{graphicx}
    \begin{document}

    \begin{table}
    \resizebox{\textwidth}{!}{%
      \begin{tabular}{cc}
        Knuth & Lamport
      \end{tabular}}
    \end{table}

    \end{document}

Big advantage is that it scales everything, so the table still looks nice :)

## Todo Notes

List all todos

    \listoftodos

## ticks the same

In order to have the same spacing for the ticks in a plot, use

    - axis equal        -> will make the axis units same while keeping the dimensions (usually what you want)
    - axis equal image  -> will make the axis units same, but does not keep the plot dimensions.

Just add the desired option in the beginning of the tikz plot, right after

    \begin{axis}[%
    <here>,
    ...
    \end{axis}

## Displaying code

Thanks to stackexchange, there are already premade templates in how to display code in latex.
What follows is a collection of environments to display code.

    %------------------------------------------------------------------------------%
    % For displaying Python Code
    % The python envorinment is called with \begin{python} \end{python}
    %------------------------------------------------------------------------------%
    % Default fixed font does not support bold face
    \DeclareFixedFont{\ttb}{T1}{txtt}{bx}{n}{8} % for bold
    \DeclareFixedFont{\ttm}{T1}{txtt}{m}{n}{8}  % for normal

    \usepackage{listings}
    \usepackage{color}
    \definecolor{deepblue}{rgb}{0,0,0.5}
    \definecolor{deepred}{rgb}{0.6,0,0}
    \definecolor{deepgreen}{rgb}{0,0.5,0}
    % Python style for highlighting
    \newcommand\pythonstyle{\lstset{
    language=Python,
    basicstyle=\ttm,
    otherkeywords={self},             % Add keywords here
    keywordstyle=\ttb\color{deepblue},
    emph={MyClass,__init__},          % Custom highlighting
    emphstyle=\ttb\color{deepred},    % Custom highlighting style
    stringstyle=\color{deepgreen},
    frame=tb,                         % Any extra options here
    showstringspaces=false            %
    }}


    % Python environment
    \lstnewenvironment{python}[1][]
    {
    \pythonstyle
    \lstset{#1
      breaklines=true,
      postbreak=\mbox{\textcolor{red}{$\hookrightarrow$}\space},}
    }
    {}
    %------------------------------------------------------------------------------%

## Placing Legend Outside tikz plot

    legend pos=outer north east,
    legend cell align=left,

Just add these two lines (usually only the first one) in the legend style option 
of your tikz plot file and, tadaa, the legend is outside the plot.

## Indexing
