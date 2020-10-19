# Moinuddin Ahmad
# 10/16/2020

from collections import defaultdict, namedtuple
import math
from queue import PriorityQueue
import sys


def build_path(came_from, i):
    path = [i]
    current = i
    while current in came_from:
        path = [came_from[current]] + path
        current = came_from[current]
    return path


def shortest_path(graph, start, goal):
    def distance(a, b):
        x0, y0 = graph.intersections[a]
        x1, y1 = graph.intersections[b]
        return math.sqrt((x1 - x0) ** 2 + (y1 - y0) ** 2)

    def h(i):
        return distance(i, goal)

    def debug(level, *args):
        # print '  ' * level, args
        return

    q = PriorityQueue()
    q.put((h(start), 0, start))

    open_set = set([start])

    came_from = {}

    g_score = defaultdict(lambda: sys.maxsize)
    g_score[start] = 0

    f_score = defaultdict(lambda: sys.maxsize)
    f_score[start] = h(start)

    while open_set:
        _, level, current = q.get()
        open_set.remove(current)
        debug(level, 'current', current, 'neighbors', graph.roads[current])
        if current == goal:
            return build_path(came_from, current)
        for neighbor in graph.roads[current]:
            debug(level, 'neighbor', neighbor)
            tentative_g_score = g_score[current] + distance(current, neighbor)
            debug(level, 'tentative_g_score', tentative_g_score, 'g-score', g_score[neighbor])
            if tentative_g_score < g_score[neighbor]:
                came_from[neighbor] = current
                g_score[neighbor] = tentative_g_score
                f_score[neighbor] = g_score[neighbor] + h(neighbor)
                debug(level, 'current', current, 'neighbor', neighbor, 'g_score', g_score[neighbor], 'f_score', f_score[neighbor])
                if neighbor not in open_set:
                    q.put((f_score[neighbor], level+1, neighbor))
                    open_set.add(neighbor)
    raise Exception("failure")
