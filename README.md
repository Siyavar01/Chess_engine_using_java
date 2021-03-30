# Chess_engine_using_java

# ABSTRACT:

This project is based on making a chess game/engine using Object Oriented
Programming (OOP’S) concept in Java.
It will provide the user with the option of playing a game of chess with another player

or the computer/system itself.
We’ll be working on IntelliJ IDEA and make use of Java-JDK.
Graphic User Interface (GUI) and Minimax algorithm in Artificial Intelligence (AI)
will be employed to achieve the same.


# INTRODUCTION
# PROBLEM DEFINITION:

The problem is to design a Chess Game using Object Oriented Principles.
The main classes will be:
• Spot: A spot represents one block of the 8×8 grid and an optional piece.
• Piece: The basic building block of the system, every piece will be placed on a
spot. Piece class is an abstract class. The extended classes (Pawn, King,
Queen, Rook, Knight, Bishop) implements the abstracted operations.
• Board: Board is an 8×8 set of boxes containing all active chess pieces.
• Player: Player class represents one of the participants playing the game.
• Move: Represents a game move, containing the starting and ending spot. The
Move class will also keep track of the player who made the move.
• Game: This class controls the flow of a game. It keeps track of all the game
moves, which player has the current turn, and the result of the game.
Later, we’ll integrate the GUI & AI into our program in order to
successfully solve the problem.

# Hardware Specification:
No such requirements.
Software Specification:
IntelliJ IDEA and Java-JDK Version 14.

# SYSTEM ANALYSIS AND DESIGN:
Step by Step Overview of the Algorithm
Step 1: Introduce Tile class representing a given tile on the board.
Step 2: Now introduce Piece class which will contain sub-classes Bishop, Knight,
Rook, King, Queen and Pawn. These classes will contain the implementation of the
legal moves for the said piece respectively.
Step-3: Fleshing a new and very important class i.e. Move class. It’ll contain the
implementation for executing a move over the board.
Step 4: Introducing the Board class which will build the chessboard containing 64
tiles and all of the 32 pieces i.e. 16 of both white and black.
Step 5: Implementing the Player class which will contain sub-classes white Player and
black Player. It’ll do the move generation for white and black pieces.
Step 6: Working on the GUI which’ll have taken Pieces Panel, game History Panel
and options to quit a game and highlight Legal Moves.
Step 7: Building on the Mini Max Algorithm of AI by introducing the necessary
classes. In the end, connecting the AI to the GUI.
Step 8: Preparing and running Test cases.

# TESTING PROCESS

We've developed a test case i.e TestBoard which checks whether all the pieces are
rightly placed over the board or not and also whether a said piece can move in a
correct (legal) manner. We've also developed a test case i.e testfoolsmate which
checks the accuracy of our AI which we've implemented by using the MinMax
algorithm of AI. The code for the same is as follows:
package com.tests.chess.engine.board;
import com.chess.engine.board.Board;
import com.chess.engine.board.BoardUtils;
import com.chess.engine.board.Move;
import com.chess.engine.player.MoveTransition;
import com.chess.engine.player.ai.MiniMax;
import com.chess.engine.player.ai.MoveStrategy;
import org.junit.Test;
import static com.chess.engine.board.Move.CastleMove.*;
import static org.junit.Assert.*;
public class TestBoard {
@Test
public void initialBoard() {
final Board board = Board.createStandardBoard();
assertEquals(board.currentPlayer().getLegalMoves().size(), 20);
assertEquals(board.currentPlayer().getOpponent().getLegalMoves().size(), 20);
assertFalse(board.currentPlayer().isInCheck());
assertFalse(board.currentPlayer().isInCheckMate());
assertFalse(board.currentPlayer().isCastled());
//assertTrue(board.currentPlayer().isKingSideCastleCapable());
//assertTrue(board.currentPlayer().isQueenSideCastleCapable());
assertEquals(board.currentPlayer(), board.whitePlayer());
assertEquals(board.currentPlayer().getOpponent(), board.blackPlayer());
assertFalse(board.currentPlayer().getOpponent().isInCheck());
assertFalse(board.currentPlayer().getOpponent().isInCheckMate());
assertFalse(board.currentPlayer().getOpponent().isCastled());
//assertTrue(board.currentPlayer().getOpponent().isKingSideCastleCapable());
//assertTrue(board.currentPlayer().getOpponent().isQueenSideCastleCapable()
);
//assertEquals(StandardBoardEvaluator.evaluate(board, 0), 0);
}
@Test
public void testAI() {
final Board board = Board.createStandardBoard();
final MoveStrategy moveStrategy = new MiniMax(4);

final Move move = moveStrategy.execute(board);
System.out.println(move);
}
@Test
public void testFoolsMate() {
final Board board = Board.createStandardBoard();
final MoveTransition t1 = board.currentPlayer()
.makeMove(MoveFactory.createMove(board,

BoardUtils.getCoordinateAtPosition("f2"),

BoardUtils.getCoordinateAtPosition("f3")));

assertTrue(t1.getMoveStatus().isDone());
final MoveTransition t2 = t1.getTransitionBoard()
.currentPlayer()
.makeMove(MoveFactory.createMove(t1.getTransitionBoard(),

BoardUtils.getCoordinateAtPosition("e7"),

BoardUtils.getCoordinateAtPosition("e5")));

assertTrue(t2.getMoveStatus().isDone());
final MoveTransition t3 = t2.getTransitionBoard()
.currentPlayer()
.makeMove(MoveFactory.createMove(t2.getTransitionBoard(),

BoardUtils.getCoordinateAtPosition("g2"),

BoardUtils.getCoordinateAtPosition("g4")));

assertTrue(t3.getMoveStatus().isDone());
final MoveStrategy strategy = new MiniMax(4);
final Move aiMove = strategy.execute(t3.getTransitionBoard());
final Move bestMove = MoveFactory.createMove(t3.getTransitionBoard(),
BoardUtils.getCoordinateAtPosition("d8"),

BoardUtils.getCoordinateAtPosition("h4"));
assertEquals(aiMove, bestMove);
}
}


# CONCLUSIONS


This project is based on making a chess game/engine using Object Oriented Programming
(OOP’S) concept in Java.
It provides the user with the option of playing a game of chess with another player or the
computer/system itself.
We’ve developed it on IntelliJ IDEA and also made use of Java-JDK.
Graphic User Interface (GUI) and Minimax algorithm in Artificial Intelligence (AI) are
employed to achieve the same.
